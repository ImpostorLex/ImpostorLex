# Bandit Level 21 - 34
---

## Bandit 21
The password on **Bandit 20**: **gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr**.

```ad-question
A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.
```

**cron** is a command-line utility that allows to schedule jobs, scripts, or commands.

After switching to **/etc/cron.d/**(**d** stands for daily, so there are months, hours, mins). 

Each file shows **5 Asterisk** meaning that they will run for every minute of every day of every week of every month.

![[Pasted image 20220728180708.png]]

![[Pasted image 20220728180941.png|center]]

**&>** redirects output and standard error into **/dev/null** which discards everything written to it. 

On directory **/usr/bin/cronjob_bandit22**.

![[Pasted image 20220728181543.png]]
The rest is empty.

`chmod 644` indicates that owner of file have read and write access while group and others have only read access.

```bash
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

**Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI**

---

## Bandit 22

```ad-question
A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

**NOTE:** Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.
```

Almost the same result at the previous level.

Found in **/usr/bin/cronjob_bandit23**.

![[Pasted image 20220728191908.png]]

According to the image we can execute the script as the group since we are part of the  group bandit22.

![[Pasted image 20220728185636.png]]

What the code does is it takes `whoami` command as input to a parameter indicated by the **$** sign into a variable called **myname**, the **mytarget** do is take "I am user bandi22" as the input for **md5sum** which is a hashing algorithm and then takes the **hashed** text to **cut -d** represents that the empty space is the seperator then `-f 1` cut only the first field for each line.

Hash output example: **asdasda** dasdasda asdasdas 
Since the **'  '**  or space represents the seperator then the flag `-f 1` will only save **asdasda** then the rest is discarded.

Since bash script file `whoami` command will output **bandit22** we need to change it to 23.

```bash
echo I am user bandit23 | md5sum | cut -d ' ' -f 1
```

returns a file called:- **8ca319486bfbbc3663ea0fbe81326349**.

```bash
cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```

returns password:- **jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n**.

---

## Bandit 23

```ad-example
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…
```

```bash
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
	# tells the script to ignore '.' and '..' directory.
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```
