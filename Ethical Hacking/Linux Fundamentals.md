# Linux

- Is a term for multiple OS's that are based on UNIX (also an OS), Linux is a open source since UNIX is open source too.

- Many Linux comes in all shapes and sizes.

- The two most common are Ubuntu and Debian.

- First release of Linux OS is year 1991.

---
## Basic Commands

- `echo` used to output any text.

- `whoami` show who is currently logged-in.

-  `ls directory` show a list of items inside that directory without going to that directory.

- `find -name filename` find the path of specified filename.

- `grep "value to be questioned" filename` find specific value from the specified file.

- `&` allows to execute commands from the background.

- `&&` allows to use two or more commands on the same line.

- `>` redirects the content of a file to another file (without the single quotes).

- `>>` append content in a file .

---
## Remote Access

- `SSH` or Secure Shell is a protocol that sends any input into a encrypted text (unreadable) and decrypts it after reaching destination

- Connects and interacts with the command line of another remote machine var(--text-highlight-bg) var(--text-normal)

```ad-example
title: SSH Syntax
The syntax is username seperated by @ sign then the IP address.
==ssh tryhackme@10.10.217.100==

Another example using an URL instead of an IP address but needs a port number specified by the server.
==ssh bandit0@bandit.labs.overthewire.org -p 2220==

```
- Most of the tools that we used on Linux's Terminal have arguments and these arguments allow certain keywords known as **flag** or **switches**

-  We can find out more about the machine that we are trying to remote access by using the list command` ls -lh` this shows the files in that directory and who or what user it belongs to.

- Once that we identified some of the users in that machine we can switch to that users by using the command `su username`, then you will be prompted for password.

- These are the most important and common directories that can be found on a Linux system.
	
	- **/etc** is one of the root directory is a common place to store system files that are used by the operating system.
	- **/var** also one of the root directory that stores data that is always used or written by services and applications running on the system.
	- **/root** is the home directory of the root system user.
	- **/tmp** stores data that are used once or twice once the computer is restarted files are wiped out.
		- As a pentester this is a great place to store  things like enumaration scripts.
---

## Process 101

- Process are programs that runs on our machine, it is managed by the kernel, and each process have PIDs, and PIDs are incremented in order. 

- We can show what processes are running using the command `ps` and we can show all processes running including the system process using `ps aux`.

- We can see real time processes using `top`

-  Operating system uses namespaces to split up resources available on the compuer (such as CPU, RAM, and priority) process, Only in the same namespace can see each other.

- **PID 0** is a process that starts when the system boots-up and these processes that run without even user's executing it is called 'daemons' 

- Once the system  boots up and inialises, the **systemd** (provides a way of managing user's process and it is located between the OS and the user.) is the first process that will run. Any software or program will run under systemd but it will run as its own process meaning new specfic PID for that process.

---

### Killing A Process
- We can kill a process using `kill PID#` or we can let it do something before killing it.
	
	• `SIGTERM` - Kill the process, but allow it to do some cleanup tasks beforehand.
	
	• `SIGKILL` - Kill the process - doesn't do any cleanup after the fact.
	
	• `SIGSTOP` - Stop/suspend a process.

---

### Systemctl 
- We can start, stop, enable, and disable processes when it boots up using `systemctl`

```ad-example
title: Systemctl
**systemctl start apache2**
```
- Processes can run in the background or foreground by typing a command and followed by `&` at the end of the command the command specified will be run in the background and we can also bring it back to foreground using `fg`

---

## Maintaining Your System
- Apt is a software

- **.gpg** is an extension for a file, it stands for Gnu Privacy Guard, is a key, whenever a user tries to download through apt the software developer will give a key to the user if the key matches the software is downloaded if not then it is canceled. (Key is matched up to what your system trust.) 

- Every installation should be `sudo apt update` so the installation can be recognized

- We can see our system logs in directory **/var/log** 



---
Beginner to Advanced Linux CTF [[Bandit 1-20|OverTheWire's CTF]]
