# OverTheWire
A CTF game or Capture the flag game wherein the flag is the password to move up to the next level.

Uses ssh to connect to the command line of a remote machine.

`ssh bandit0@bandit.labs.overthewire.org -p 2220`

## Bandit0
Password in readme.txt file: **boJ9jbbUNNfktd78OOpsqOltutMc3MY1**

---
## Bandit1
Opened a filename ''-'' using **.cat /-** to open a dashed file **CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9**

---
## Bandit2
Uses quotes  to open filename with spaces. `cat 'spaces in this file name'` 
**UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK**

---
## Bandit3
Uses `ls -la` to reveal a long list format and all hidden files.

Found a file *.hidden* uses a text editor `nano .hidden` to reveal password: **pIwrPrtPN36QITSp3EQaw936yaFoFgAB**

---
## Bandit4
cat **./-file07** : **koReBOKuIDDepwhWk7jZC0RTdopnAYKh**

---
## Bandit5
Is human readable, 1033 bytes in size, not executable

found on dir **maybehere07 : ./file2** : **DXjZPULLxYr17uwoI01bNLQbtFemEgo7**

---
## Bandit6
We don't know the directory only the parameters.

owned by user bandit7

owned by group bandit6

33 bytes in size

On root directory use command `find ./ -user bandit7 -group bandit6 -size 33c`

`cat lib/dpkg/info/bandit7.password`  : **HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs**

---
## Bandit7
found a file with thousands of words.

password is next to millionth.

use **grep “millionth” data.txt** : **cvX2JJa4CFALtqS87jk27qwqGhBM9plV**

---
## Bandit8
data.txt with thousand of duplicated lines with one non-duplicated line

**|** - a single pipe, takes standard output of one process then pass it as standard input into another process.

`cat data.txt | sort | uniq -u` : **UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUh**R

*uniq* cannot detect duplicate lines so that is why we need to sort it first then use *uniq -u* to only print unique lines.

---
## Bandit9
The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.

If file is binary means it is not plaintext ASCII file.

We can use **grep -a** for patterns and **strings** for contents of non-text files

![[Pasted image 20220717230208.png]]

`strings data.txt | grep -E "=+"`  : **truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk**

---
## Bandit10
data.txt file is encoded in Base64 which is an encoder

`cat data.txt | base64 -d`  : **IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR**

*-d* decodes

---
## Bandit11

The password for the next level is stored in the file **data.txt**,where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

Tr - translates the given string back to its original position since it is rotated by 13

we specified N-Z which N position is 1 and Z is 13 same as A position is 1 and M is 13th

Since we are passing a standard output using **single pipe |** to **tr**, tr will take it as standard input

then the ‘A-Za-z’ found on the data.txt will be translated according to the second argument.

`cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'` : **5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu**

---
## Bandit12
The password for the next level is stored in the file **data.txt**,which is a hexdump of a file that has been repeatedly compressed.For this level it may be useful to create a directory under /tmp inwhich you can work using mkdir. For example: mkdir /tmp/myname123.Then copy the datafile using cp, and rename it using mv (read themanpages!)

data.txt is a gunzip file.

uses `mv test.txt test2.gz `to make it gunzip 

Then decompress it using `gzip -d test2.gz`

After that test2 is extracted after checking file type using `file test2` 

it is a bzip2 compressed data.

after running `bzip2 -d test2 ` to decompress it, 

it produces a file of `test2.out `it is a gzip compressed data.

`mv test2.out test22.gz` to able to decompress again.

`test22 `is a POSIX tar archive

`tar -xf test22`

The *x* is to extract the data and *f* is to specify the file

result into POSIX tar archive again data5.bin do the same again.

`tar -xf data5.bin` results into data6.bin again, data8.bin

data8.bin is a gzip

rename again using` mv data8.bin binary.gz`

gzip -d binary.gz results into binary ASCII plaintext after using `file binary`

Finally the password is: **8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL**

---

## Bandit13

^a848e9

```ad-question
The password for the next level is stored in **/etc/bandit_pass/bandit14 and can only be read by user bandit14**. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. **Note:** **localhost** is a hostname that refers to the machine you are working on.
```

```ad-note
title: Localhost
Allows the local computer to connect and communicate with itself using an IP connection. 

More info on localhost [here](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwi91I3pqIz5AhWeqFYBHVHGBbQQmhN6BAg3EAI&url=https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FLocalhost&usg=AOvVaw1cmdfysPZv6n84W4oP5K0J)
```

Public key is used to lock messages while the private key is used to unlock the message. Typically the private key is stored in the computer you log in from and the public key is stored in the computer you want to log in to.

More about this at https://help.ubuntu.com/community/SSH/OpenSSH/Keys.

`ssh -i sshkey.private bandit14@localhost`

The `-i` flag is to identify a file to be used.

**4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e**

---

## Bandit 14
```ad-question
The password for the next level can be retrieved by submitting the password of the current level to **port 30000 on localhost**.
```

Localhost is a hostname and usually the IP address is 127.0.0.1.

and the tool **netcat** allow to read and write data over a network connection.

**netcat** allows users to transfer files between users.

![[Pasted image 20220720181939.png]]

Note: The IP address method works too.

**BfMYroe26WYalil77FoDi9qh59eK5xNr**

---

## Bandit 15
```ad-question
The password for the next level can be retrieved by submitting the password of the current level to **port 30001 on localhost** using SSL encryption.

**Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…**
```

OpenSSL is used for secure communication (encryption of data) over the network it is mostly used by applications, remote login, and HTTPS websites.

**Connectedf Commands** refers to `openssl s_client` connects to a remote host using SSL/TLS.

**-connect host:port**:- Self explanatory.

**-ign_eof**:- prevents shutting down of connection when end of file is reached in input.

`openssl s_client -connect localhost:30001 -ign_eof`

**cluFn7wTiGryunymYOu4RcffSxQluehd**

---

## Bandit 16
```ad-question
The credentials for the next level can be retrieved by submitting the password of the current level to **a port on localhost in the range 31000 to 32000**. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.
```

![[Pasted image 20220720212735.png]]

Port 31691 responded.

-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----

` nmap -sV -T4 -p 31000-32000 localhost` returns the same result but with service and version.

`-sV`:- Version of the service and service.
`-T4`:- speed up the scan.

`chmod 400 bandit16.private ` - gives the file a read permission.

Command from [[Bandit 1-20#^a848e9| Bandit 13]] is used.

`ssh -i bandit16.private bandit17@localhost`

--- 

## Bandit 17

```ad-question
There are 2 files in the homedirectory: **passwords.old and passwords.new**. The password for the next level is in **passwords.new** and is the only line that has been changed between **passwords.old and passwords.new**

**NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19**
```

Used a command called `diff`

Got this.
42c42
##### kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
##### w0Yfolrc5bwjS4qw5mq1nnQi6mF03bii
![[Pasted image 20220720215046.png]]

`<` represents the line that is added to its place.

`>` removed.

---

## Bandit 18
**Byebye !**

```ad-question
The password for the next level is stored in a file **readme** in the homedirectory. Unfortunately, someone has modified **.bashrc** to log you out when you log in with SSH.
```

As it said that we cannot currently login with the shell that we are commonly using which is **.bashrc** every time we load the terminal bashrc (the file) is loaded. 

Check `cat /etc/shells` to check all valid shells.

![[Pasted image 20220721215951.png]]

`-t` specify the shell that we are going to use.

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 -t /bin/sh
```

**IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x**

---

## Bandit 19

```ad-question
To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.
```

There are two types of set one is `setuid` and `setgid` (short for user identity and group identity).

It allows user to run an executable with the file system permission if the file belongs to the user it can run it or if the file belongs to a group that the user belongs to it can do something about it depends on the permission.

In short these two commands are needed for task that requires different privileges.

Typically when the file is run it will not "be who executed the file" rather it will be named to whoever owns the file.

More info [here](https://en.wikipedia.org/wiki/Setuid).

---

After running `file bandit20-do`.
![[Pasted image 20220722195225.png|700]]

Is set as **setuid** everytime another user execute it (with permission of course) it will be run by the owner of the file not the one who is executing it.

After running `ls -la` , the file **bandit20-do** 

![[Pasted image 20220722210017.png|650]]

**setuid** allows the user to give a special type of permission that can be given to a file which is in this case its the **bandit20-do**.

```ad-note
title: Access permisson have an S
The **s** in the row with bandit20-do is indicated as SUID.
```

`./bandit20-do cat /etc/bandit_pass/bandit20`
**GbKksEFF4yrVs6il55v6gwY5aVje5f0j**

---

## Bandit 20

```ad-question
There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

**NOTE:** Try connecting to your own network daemon to see if it works as you think
```

![[Pasted image 20220723193651.png|900]]

```Bash
echo -n 'GbKksEFF4yrVs6il55v6gwY5aVje5f0j' | nc -l -p 12345&
```

`netcat -l` can be used to create a server and `-p ####` can be used as the port number. The `-l` flag stands for **listening**, will listen to connection to the specified **port** number (in this case we are sending a string to whoever connects to port 12345).

As specified in the **question**, the **suconnect** file will connect to a localhost on what the specified port is.

```Bash
./suconnect 12345
```

**gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr**

---

Bandit Map of Content [[Bandit  MOC|here]].
Bandit Level 20-34 [[Bandit 21-34|here]].
