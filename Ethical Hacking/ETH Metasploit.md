# Metasploit
Is a set of tools that allows for information gathering, scanning, exploitation, exploit development, post-exploitation, and more.

Built-in Kali Linux on the command line using `msfconsole` to bring up metasploit.

The tools or scripts that we used are called `modules` they are built to performa specific task.

#scripts_vs_codes

- **Exploit**
	- Taking advantage of a vulnerability on a target system by using codes.

- **Vulnerability**
	-  A flaw or any type of mistake that leaves a target system vulnerable.

- **Payload**
	- Scripts or codes that will run on the target system.
	
	- Exploit is only taking advantage of a vulnerability but no result is guaranteed. (By results gaining root/admin acces, reading confidential information and such)

---

The modules can be found on directory (In Kali Linux) `/usr/share/metasploit-framework/modules/` resulting in categories.

### Auxiliary
A module that is not an exploit is an auxiliary (fingerprinting and vulnerability scanning).

In the modules category to see a treeview of all modules `tree -L 1 auxiliary/`.

![[Pasted image 20220719195628.png]]

---

### Encoders
Rewrites a exploit and payload into something unclear and hoping a *signature based antivirus* may miss them.

Antivurs have a database where they compare incoming files to their database of suspicious files and raise an alert if it is a match.

Most AVGs can perform additional checks.

`tree -L 1 encoders/`.

![[Pasted image 20220719200618.png]]

---

### Evasion
Encoder is not considered as "evasion" when it comes to evading a AVGs

Modules in evasion have more or less success.

![[Pasted image 20220719200801.png]]

---

### Exploits
Abuses the vulnerability found on the target system by using codes.

![[Pasted image 20220719201019.png]]

---

### NOPs (No OPeration)

Does nothing.

`tree -L 1 nops/`

---

### Payloads

Use to get desired results by sending a piece of code to the said exploit for acheiving desired results.

Examples are loading a malware, creating a backdoor to the target system or executing calc.exe remotely just to show that you gained access and can control the system remotely.

`tree -L 1 payloads/`
![[Pasted image 20220719202732.png]]

- Three different directories.
	- **Singles**:- Payloads that dont need an additional components to download, to run. Such as add user, launch notepad.exe and more.
	
	- **Stagers**:-  Sets up a connection channel between metasploit to the target system usually payloads that are sent are the stagers (to ready everything) for the rest of the payload to be sent at once.
	
	- **Stages**:- Is downloaded by the stager, Allows for large size payloads.

```ad-tip
title: Identify single payloads from staged payloads
- generic/shell_reverse_tcp
- windows/x64/shell/reverse_tcp

The former is a singe payload indicated by the "-" between the "shell" and the "reverse" while the latter is staged indicated by the "/" and "shell" and "reverse"
```
	
---

### Post

After succesfully intruding a system. Post modules are useful for gathering more evidence and getting deeper access to the network.

![[Pasted image 20220719204052.png]]

---

### Msfconsole
The terminal will changed after running the command `msfconsole`.

Will support most [[Linux Fundamentals|Linux]] commands but does not support output redirection, e.g `help > help.txt`

Just as most Linux commands that have a help menu so does the command for msfconsole, e.g `help set`.

Unless set as global variable whenever we changed modules we have to insert the parameters again.

We can use a module by using `use` command followed by the number in the beginning of the result or the vulnerability name.

`show options` will show all parameters from required to optional that is needed to be filled and `info` will show more further information (such as author, relevant sources, etc) on a specific module.

the `show payloads`  (or any categories previously mentioned) another way to show all available tools.

The `search` will output result related to the given search parameter such as [CVE](https://cve.mitre.org/) numbers (Common Vulnerabilites Exposure), exploit names (eternalblue, samba, etc), or target systems.

And search results return exploits and such with rankings on how effective they are.
![[Pasted image 20220719215552.png]]

We can `unset` all parameters or just one using `unset {parameter_here}`

We can set values for all modues without losing it once switching via `setg` command.

```ad-example
title: setg
**setg RHOST x.x.x.x** to unset simply **unsetg RHOST**
```

We can `background` a session using `background` command and open up a new session to interact with multiple session we can use `session -i n` where **n** is the id number.

- **RHOSTS:** “Remote host”, the IP address of the target system. A single IP address or a network range can be set. This will support the CIDR (Classless Inter-Domain Routing) notation (/24, /16, etc.) or a network range (10.10.10.x – 10.10.10.y). You can also use a file where targets are listed, one target per line using file:/path/of/the/target_file.txt, as you can see below.
![[Pasted image 20220719221304.png|800]]
-   **RPORT:** “Remote port”, the port on the target system the vulnerable application is running on.
-   **PAYLOAD:** The payload you will use with the exploit.
-   **LHOST:** “Localhost”, the attacking machine (your AttackBox or Kali Linux) IP address.
-   **LPORT:** “Local port”, the port you will use for the reverse shell to connect back to. This is a port on your attacking machine, and you can set it to any port not used by any other application.
-   **SESSION:** Each connection established to the target system using Metasploit will have a session ID. You will use this with post-exploitation modules that will connect to the target system using an existing connection.

---

More tools [[Ethical Hacking MOC#^17ad72|here]].
