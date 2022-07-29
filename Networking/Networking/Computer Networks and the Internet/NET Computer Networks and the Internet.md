```toc
style: number
min_depth: 1
max_depth: 6
```

Up::[[Networing MOC|Map Of Content]]
Tags:: #on/Internet
Date:: 07/29/2022

---

# What Is The Internet
Is  a computer network that interconnects billions of computing devices.

Host are devices that are connected to the Internet.

![[Pasted image 20220630102336.png|Test]]
Some pieces of the Internet.

## Hosts
Is connected together by a network of *Communication Links* and *Packet Switches*.

- Access the internet through their Internet Service Provider.
	- Residential ISPs (local cable or telephone companies)
	- Corporate ISPs
	- University ISPs
	- ISPs that provided WiFi access in airports, coffee shops, etc and cellular data ISPs that provided mobile access to the internet.

---

## Communication Links

^4cb2f0

- Made up of different types of physical media
	- Coaxial cable
	- Copper wire
	- Optical fiber
	- Radio Spectrum
	
Different links have different data transmission rates, transmission rate is measured in bits/seconds.

When an end system sends a data, it segments the data and adds #header bytes to each segments thus resulting into packets then send to the destination specified in the header and segments are reassembled back to the original form.

---

## Packet Switches 

^4b036a

Many types of packet switches but two most common are *routers* and *link-layer switches* both forwards packets into their destination.

Packets that travels in order of communication links and packet switches from sender to receiver is known as route or path.

- An example of this in a real world scenario is a commercial trucks, factory wants to move large amount of cargo, cargo is segmented and loaded to fleet of trucks, trucks travels to network of highways, trucks reached destination, cargo unloaded and grouped with the other cargos.

	- Sender and Receiver warehouse = end systems
	- Trucks = packets
	- Highways or Road = communication links
	- Intersections = packet switches

---

## Internet Service Providers
^f4e7d1
Is a network of packet switches and communication links.

Provides types of network access using residential broadband access such as cable modem or DSL, high-speed LAN access, and mobile wireless access.

Connects content provider's servers directly to the Internet such as Facebook, Twitter, and Instagram.

Low-tier ISPs are connected to national and international upper-tier ISPs and upper-tier ISPs are connected directly to each other, an upper-tier ISP consists of high speed routers interconnected with high-speed fiber-optic links.

---
## Internet
Hosts, packet switches and other pieces of the internet run *Protocols* that controls the sending and receiving of information within the internet.

Internet apps includes mobile and tablet applications such as social media, music, television, and movie streaming these are what you call Distributed applications they involve multiple end systems that exchange data with each other. 

Apps run on end systems not on packet switches.

---

## Socket Interface
Is a set of rules that a program must follow so the Internet can deliver the data.

Specifies how a program running on one hosts asks the Internet infrastructure to deliver the data into a specific destination program running on another hosts.

- A real life example:
	- Alice wants to send a letter (the data) to Bob using a postal service and the postal service has its *set of rules* when it comes to sending a letter, It requires the letter to be inside of the envelope, Alice and Bob's full name, address, and zip code and drop it into the postal service mailbox.
	
	- A postal service has more than one services other than sending and receiving letters, it provides express delivery, reception confirmation, and more. Similarly the Internet provides multiple services to its applications.
	
---

## Protocols
- Greetings between two (or more) communicating entities running on the same protocols
	- Sometimes different response to an 'Hi' is 'Don't bother me!' therefore we cannot proceed to ask a question or do something we intended to do with that person (or computer). 
	
	- In other words two (or more) entities should be acknowledge each other first and must be running on the same protocol.
	
- All communicating activities between entities are governed or ruled by protocols.
	- Hardware-implemented protocols in two physically connected computers control the flow of bits on the 'wire' between two #network_interface_card. 
	
	- Congestion-control protocols in *hosts* controls the rate at which packets are transmitted between sender and receiver	
---

Continues [[NET Network Edge|here]].







 








 



