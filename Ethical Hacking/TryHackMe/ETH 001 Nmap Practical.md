# Practical NMAP

Target Machine's IP: 10.10.43.103

Examples:

	`nmap -sn 192.168.0.1-254`
	
	 `nmap -sn 192.168.0.0/24`

Does the target (`10.10.43.103`)respond to ICMP (ping) requests (Y/N)?
**No**
![[Pasted image 20220718212121.png]]

Perform an Xmas scan on the first 999 ports of the target -- how many ports are shown to be open or filtered?
`nmap -p 1-999 -sX 10.10.43.103`
![[Pasted image 20220718212627.png]] 

There is a reason given for this -- what is it?

The answer will be in your scan results. Think carefully about which switches to use?
`nmap -p 1-999 -sX 10.10.43.103 -vv`
![[Pasted image 20220718213244.png]]

`-vv` flag or switch does is give more information without `-v` only the critical information is shown the more `-v` in the flag will show more information but much noiser.

Perform a [[ETH Nmap#^729937|TCP SYN]] scan on the first 5000 ports of the target -- how many ports are shown to be open?
`nmap -sS 5000 10.10.43.103 -vv`
![[Pasted image 20220718213859.png]]

Open Wireshark (see [Cryillic's](https://tryhackme.com/p/Cryillic) [Wireshark Room](https://tryhackme.com/room/wireshark) for instructions) and perform a [[ETH Nmap#^0b4ca7|TCP Connect scan]] against port 80 on the target, monitoring the results. Make sure you understand what's going on.

Run wireshark and `nmap -sT -p 80 10.10.43.103`.

On Wireshark, Double click 'eth0' interface. (Demo done through my own VM.)

![[Pasted image 20220718220600.png]]

Included the Target's IP in the green highlight.

Ran nmap on terminal with `nmap -sT -p 80 192.18.57.4`

On Wireshark after running the nmap command
![[Pasted image 20220718221614.png|1500]]

Source: 192.168.100.4 sends a SYN flag at dest. 192.168.57.4 using TCP protocol.
Then Dest. responds with SYN/ACK flag set after that source responds with ACK flag set.
Then source respond or receives (not sure between the two) a RST/ACK flag set.


Deploy the `ftp-anon` script against the box. Can Nmap login successfully to the FTP server on port 21? (Y/N) **Y**

`nmap --script=ftp-anon 10.10.43.103`
![[Pasted image 20220718215957.png]]


---

Tools used [[ETH Nmap|here]].
