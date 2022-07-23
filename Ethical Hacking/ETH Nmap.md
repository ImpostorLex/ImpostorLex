```toc
```
# Nmap
Before launching an attack we need to know first what is the landscape of what we are attacking.

Whenever a computer running a network service it uses a port to get or to make requests on a server and then opens a port to listen on the server we connected to.

```ad-example
title: Port 80
Connecting to a unencrypted websites uses Port 80, the user who iniates a connection to the server is the source then your machine opens up any random port to listen or get/receive information in this case webpages.
```

- In order for client and server to know that they are both ready to transfer/receive data it uses the *Three way handshake*.

	-  Our client sent an SYNCHRONIZE flag then the server acknowledges this packet with a TCP response containting the SYN flag and Acknowledge flag then the sender completes the handshake sending a TCP request with the ACK flag set.

---

## TCP Connect Scans

^0b4ca7

The command `nmap -sT` performs the three way handshake in all specified ports in turn and determines wether the port is open based on the response.

In order for nmap to tell if a port is closed is by sending a SYN flag then the server will response with RST(reset) flag set.

Most firewalls are configured to drop incoming packets. Nmap sends a TCP SYN request and receives nothing. This indicates that the port is protected by a firewall.

In Linux's IPtables we can configure a firewall to send a RST TCP packet that command would be.

```ad-example
title: IPtable firewall
iptables -I INPUT -p tcp --dport <port> -j REJECT --reject-with tcp-reset
```

---

## SYN Scans

^729937

The command `nmap -sS` are used to scan the TCP port-range of a target this scans are often referred to as "*half-open*" scans or "*Stealth*" scans.

When the one who iniates the connection receives a SYN/ACK flag set, the target is sent back a RST TCP packet so the server stops from repeating sending request.

- Advantages:
	- Can be used to bypass older intrusion Detection systems since nowadays they are looking for a full three way handshake.  No longer the case with modern IDS solutions.
	
	- Often not logged by applications listening on open ports, as a standard practice is to log a connection once it is fully established, that is SYN scans also referred stealthy.
	
	- Without needing to complete and disconnecting from a three way handshake for every port, SYN scans are much faster than TCP Connect scan.

 - Disadvantages
	 - Requires sudo permissions in order to work correctly on Linux. SYN scans require the ability to create raw packets which the root user can only do by default.
	 
	 - If client provided a test environment for the test it could be problematic since SYN scans can make services Unstable. 

If nmap is run with sudo the default will be SYN scans without sudo the TCP Connect scan is used.

---

## UDP Scans
The command `namp -sU` is a udp connection that rely on sending packets to the receiver and hoping that they are received without the SYN and ACK flags. UDP is stateless.

UDP or User Datagram Protocol is great for speed over quality such as video sharing but the lack of ACKs makes it harder to scan by nmap.

**open|filtered** is referred by nmap if a packet is sent to an open UDP port that there should be no response. nmap could suspect that the port is open but it could be blocked by the firewall, if it gets a response nmap marked it as *open*

nmap most of the time send packets for a second time as to double-check to see if there is a response, if not then it is marked as open|filtered.

The target sends back a ICMP (ping) packet containing a message that the port is unreachalable if a packet sent by nmap is sent on a closed UDP port.

With a good connection scanning with UDP scans can take 20 minutes of scanning 1000 ports, it is best practice to scan only the top 20 UDP ports.

```ad-example
title: Scanning UDP ports with top 20 only
`nmap -sU --top-ports 20 <target>`
```

---

## NULL, FIN and Xmas TCP
More stealthier than the SYN 'stealth' scan.

The command `-sN` or the NULL scan are TCP request that is sent with no flags set at all.
 ![[Pasted image 20220717213319.png]]

The command `-sF` or the FIN scan works almost the same with the `-sN` but it a request is sent with a FIN flag usually to close an active connection.
![[Pasted image 20220717213340.png]]

The command Xmas scans `-sX` sends a malformed TCP packet and expects a RST response for closed ports.
![[Pasted image 20220717213527.png]]

Nmap expects RST for both NULL and FIN commands.

These scans are useful for firewall evasion since firewall drops TCP packets with SYN flag set.

Microsoft Windows tend to respond with a RST for every port scanned.

---

## ICMP Network Scanning

Stands for **Internet Control  Message Protocol**.

On a black box assignment the first thing we should do is which IP address contain active hosts, and which do not.

We can do this by performing a nmap "ping sweep", nmap sends a ICMP packet to each possible IP address in the specified network when it receives a response nmap marks it as **alive** (not always accurate but still worth looking into).

- We can do this in two way with a `-` or CIDR notation.
	- `nmap -sn 192.168.0.1-254`

	- `nmap -sn 192.168.0.0/24`

`-sn` tells nmap to not scan any ports but rely on ICMP echo packets or in Address Resolution Protocol (ARP) on a local network if the `-sn`  is run on `sudo` the #ARP "Who has this IP address?" and the response is "This IP address is at this MAC address."

`-sn` it will also send a TCP SYN packet to port 443 of the target and TCP ACK, if the command is not run on `root` then a TCP SYN is performed sending a packet to port 80.

```ad-question
title: How would you perform a ping sweep on the 172.16.x.x network (Netmask: 255.255.0.0) using Nmap? (CIDR notation)
nmap -sn 172.16.0.0/16
```

---

## NSE Scripts

Nmap Scripting Engine is written in *Lua* programming language and it is used for many things such as scanning for vulnerabilities and automating exploits, but it is most useful in reconnaisance.

- These are the categories:
	-   `safe`:- Won't affect the target
	-   `intrusive`:- Not safe: likely to affect the target  
	-   `vuln`:- Scan for vulnerabilities
	-   `exploit`:- Attempt to exploit a vulnerability
	-   `auth`:- Attempt to bypass authentication for running services (e.g. Log into an FTP server anonymously)
	-   `brute`:- Attempt to bruteforce credentials for running services
	-   `discovery`:- Attempt to query running services for further information about the network (e.g. query an SNMP server).

More categories [here](https://nmap.org/book/nse-usage.html)

---

### Working With The NSE
To activate a script we can use the command `nmap --script` if we want to run vulnerabilities script `nmap --script=vuln` but scripts will only run on active hosts.

We can run a specific script by `nmap --script=<script-name>`, e.g `nmap --script=http-fileupload-explorer`.  

Run multiple specific scripts seperated by a comma between scripts.

Some of the script requires an arguments such as authenticated vulnerability the arguments can be given using `--script-args`.

```ad-example
title: Scripts with arguments
nmap -p 80 --script http-put --script-args http-put.url='/dav/shell.php',http-put.file='./shell.php'

The *http-put* is a script that requires two arguments one the url where to upload the file and second the file location on the disk. Arguments are seperated by **comma**.
```

Scripts have built-in help menus this is best for working locally, `nmap --script-help <script-name>`

A full list of scripts and their corresponding arguments can be found [here](https://nmap.org/nsedoc/)

---

### Searching for Scripts
We can search for scripts at the webpage of nmap [here](https://nmap.org/nsedoc/) or the local storage of a Linux system that is built-in like Kali Linux.

nmap stores its scripts at `/usr/share/nmap/scripts`.

There are two ways to search for scripts one is going to the file `/usr/share/nmap/scripts/script.db` (it is not actually a database file) or we can use the `grep` command.

```ad-example
title: Finding Scripts Using Grep
**grep "ftp" /usr/share/nmap/scripts/script.db**
![[Pasted image 20220718202438.png]]

Same technique but for categories.
**grep "safe" /usr/share/nmap/scripts/script.db**
![[Pasted image 20220718202554.png]]
```

If there are missing scripts in directory locally command `sudo apt update && sudo apt install nmap**` should fix the problem.

```ad-note
title: smb-os-discovery.nse depends on
**dependencies = {"smb-brute"}**
The `dependencies` field is an array containing the names of scripts that should run before this script, if they are also selected. This is used when one script can make use of the results of another
```

---

### Firewall Evasion

Techniques for bypassing firewalls such as stealth scans, NULL, FIN and Xmas scans.

There is a common firewall configuration that is crucial that we should know how to bypass.

A typical Windows host with its default firewall will all block ICMP packets, this means nmap will declare this firewall config as dead and not bother scanning it at all.

We can bypass this using the flag `-Pn` the command tells nmap not to ping the host and treat the target host as alive. But the problem with this it can take very long time and nmap (if host is really dead nmap will still double checking every specified port).

If you are in a Local Area Network (Network that uses switches and physical cables), nmap can make #ARP requests to determine the host activity.

- There are many switches that can be useful in firewall evasion.

	-   `-f`:- Used to fragment the packets (i.e. split them into smaller pieces) making it less likely that the packets will be detected by a firewall or IDS.
	-   An alternative to `-f`, but providing more control over the size of the packets: `--mtu <number>`, accepts a maximum transmission unit size to use for the packets sent. This _must_ be a multiple of 8.
	-   `--scan-delay <time>ms`:- used to add a delay between packets sent. This is very useful if the network is unstable, but also for evading any time-based firewall/IDS triggers which may be in place.
	-   `--badsum`:- this is used to generate in invalid checksum for packets. Any real TCP/IP stack would drop this packet, however, firewalls may potentially respond automatically, without bothering to check the checksum of the packet. As such, this switch can be used to determine the presence of a firewall/IDS.

More details [here](https://nmap.org/book/man-bypass-firewalls-ids.html)

```ad-question
title: Which simple (and frequently relied upon) protocol is often blocked, requiring the use of the *-Pn* switch?
ICMP
```

---

More tools at [[Ethical Hacking MOC#^17ad72|Level 2 - Tooling]].

 
