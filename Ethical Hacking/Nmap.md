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
The command ==nmap -sT== performs the three way handshake in all specified ports in turn and determines wether the port is open based on the response.

In order for nmap to tell if a port is closed is by sending a SYN flag then the server will response with RST(reset) flag set.

Most firewalls are configured to drop incoming packets. Nmap sends a TCP SYN request and receives nothing. This indicates that the port is protected by a firewall.

In Linux's IPtables we can configure a firewall to send a RST TCP packet that command would be.

```ad-example
title: IPtable firewall
iptables -I INPUT -p tcp --dport <port> -j REJECT --reject-with tcp-reset
```

---

## SYN Scans
The command ==nmap-sS== are used to scan the TCP port-range of a target this scans are often referred to as "*half-open*" scans or "*Stealth*" scans.

When the one who iniates the connection receives a SYN/ACK flag set, the target is sent back a RST TCP packet so the server stops from repeating sending request.

- Advantages:
	- Can be used to bypass older intrusion Detection systems since nowadays they are looking for a full three way handshake.  No longer the case with modern IDS solutions.
	
	- Often not logged by applications listening on open ports, as a standard practice is to log a connection once it is fully established, that is SYN scans also referred stealthy.
	
	- Without needing to complete and disconnecting from a three way handshake for every port, SYN scans are much faster than TCP Connect scan.

 - Disadvantages
	 - Requires sudo permissions in order to work correctly on Linux. SYN scans require the ability to create raw packets which the root user can only do by default.
	 
	 - If client provided a test environment for the test it could be problematic since SYN scans can make services Unstable. 

If nmap is run with sudo the default will be SYN scans without sudo the TCP Connect scan is used.

## UDP Scans
The command ==namp -sU== is a udp connection that rely on sending packets to the receiver and hoping that they are received without the SYN and ACK flags. UDP is stateless.

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

More tools at [[Level 2 - Tooling]].
 
