# Hydra

Hydra can use a list of username and passwords to brute force some authentication service.

Hydra has the ability to bruteforce the following protocols: 
Asterisk, AFP, Cisco AAA, Cisco auth, Cisco enable, CVS, Firebird, FTP,  HTTP-FORM-GET, HTTP-FORM-POST, HTTP-GET, HTTP-HEAD, HTTP-POST, HTTP-PROXY, HTTPS-FORM-GET, HTTPS-FORM-POST, HTTPS-GET, HTTPS-HEAD, HTTPS-POST, HTTP-Proxy, ICQ, IMAP, IRC, LDAP, MS-SQL, MYSQL, NCP, NNTP, Oracle Listener, Oracle SID, Oracle, PC-Anywhere, PCNFS, POP3, POSTGRES, RDP, Rexec, Rlogin, Rsh, RTSP, SAP/R3, SIP, SMB, SMTP, SMTP Enum, SNMP v1+v2+v3, SOCKS5, SSH (v1 and v2), SSHKEY, Subversion, Teamspeak (TS2), Telnet, VMware-Auth, VNC and XMPP.

More information about the protocols [here](https://en.kali.tools/?p=220).

Passwords should contain special and eight characters.

There are currently 100 million password lists from data breach and there is a good chance we registered our account to that services.

Here is an example if we want to brute force a protocol FTP.

`hydra -l user -P passlist.txt ftp://10.10.69.162`

Flag `-l` indicates that we are not going to need a userlist we know the username is `user`. Flag `-P` indicates we are going to give a password list.

---

### **SSH**
`hydra -l <username> -P <full path to pass> 10.10.69.162 -t 4 ssh`

It is important to make threads only to four (We can think about it as number of tries.)

![[Pasted image 20220720165349.png|center]]

---

### Post Web Form

Bruteforcing a web form is slightly different and require parameters such as is it making a GET or POST request (Note: This two methods are commonly used).

We can know what type of method is used by checking the source code using the developers tool (Right click + Inspect).

`hydra -l <username> -P <wordlist> 10.10.69.162 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V`

![[Pasted image 20220720165807.png|center]]


---

More tools [[Ethical Hacking MOC#^17ad72|here]].


