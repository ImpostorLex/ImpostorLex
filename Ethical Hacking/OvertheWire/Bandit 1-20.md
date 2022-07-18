# OverTheWire
A CTF game or Capture the flag game wherein the flag is the password to move up to the next level.

Uses ssh to connect to the command line of a remote machine.

`ssh bandit0@bandit.labs.overthewire.org -p 2220`

## Bandit0
Password in readme.txt file: **boJ9jbbUNNfktd78OOpsqOltutMc3MY1**

## Bandit1
Opened a filename ''-'' using **.cat /-** to open a dashed file **CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9**

## Bandit2
Uses quotes  to open filename with spaces. `cat 'spaces in this file name'` 
**UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK**

## Bandit3
Uses `ls -la` to reveal a long list format and all hidden files.

Found a file *.hidden* uses a text editor `nano .hidden` to reveal password: **pIwrPrtPN36QITSp3EQaw936yaFoFgAB**

## Bandit4
cat **./-file07** : **koReBOKuIDDepwhWk7jZC0RTdopnAYKh**

## Bandit5
Is human readable, 1033 bytes in size, not executable

found on dir **maybehere07 : ./file2** : **DXjZPULLxYr17uwoI01bNLQbtFemEgo7**

## Bandit6
We don't know the directory only the parameters.

owned by user bandit7

owned by group bandit6

33 bytes in size

On root directory use command `find ./ -user bandit7 -group bandit6 -size 33c`

`cat lib/dpkg/info/bandit7.password`  : **HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs**

## Bandit7
found a file with thousands of words.

password is next to millionth.

use **grep “millionth” data.txt** : **cvX2JJa4CFALtqS87jk27qwqGhBM9plV**

## Bandit8
data.txt with thousand of duplicated lines with one non-duplicated line

**|** - a single pipe, takes standard output of one process then pass it as standard input into another process.

`cat data.txt | sort | uniq -u` : **UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUh**R

*uniq* cannot detect duplicate lines so that is why we need to sort it first then use *uniq -u* to only print unique lines.

## Bandit9
The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.

If file is binary means it is not plaintext ASCII file.

We can use **grep -a** for patterns and **strings** for contents of non-text files

![[Pasted image 20220717230208.png]]

`strings data.txt | grep -E "=+"`  : **truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk**

## Bandit10
data.txt file is encoded in Base64 which is an encoder

`cat data.txt | base64 -d`  : **IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR**

*-d* decodes

## Bandit11

The password for the next level is stored in the file **data.txt**,where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

Tr - translates the given string back to its original position since it is rotated by 13

we specified N-Z which N position is 1 and Z is 13 same as A position is 1 and M is 13th

Since we are passing a standard output using **single pipe |** to **tr**, tr will take it as standard input

then the ‘A-Za-z’ found on the data.txt will be translated according to the second argument.

`cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'` : **5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu**

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


