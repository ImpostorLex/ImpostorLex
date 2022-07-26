
[[Networing MOC]]

---

# Network Core

Is a support or frame that interconnects different networks that offer many types of services.

These are the routers and switches.

---

## Packet Switching

^17c2e0

End systems exchange **messages** with each other and these messages can be whatever the application designer wants, it can also perform control actions.

These messages from the source are broken down to chunks also known as packets.

Packets travels through [[NET Computer Networks and the Internet#Communication Links|Communication Link]] and [[NET Computer Networks and the Internet#Packet Switches|Packet Switches]].

*L* represents Packet length and *R* represents link bandwidth assuming #Propagation_delay  is zero, L = 7.5Mbits and R = 1.5Mbps = it will take 5 Seconds to reach the destination.

Related [[NET Computer Networks and the Internet#^4b036a|Packet Switches]].

---
### Store-and-Forward Transmission

(Most packet switches) Entire packet must arrived first before transmission of first bit packet.

 ![[Pasted image 20220709093318.png|center]]
 
Packet 1 arrives at the Router but Router will not transmit, it is waiting for the rest of the packet, Packet 1's bits are stored or buffered.

With #Propagation_delay it depends the speed of the medium and how long the link is

- 1 Kilobyte = 1000 Byte
- 1000 Byte = 1 Kilobyte
- 1 Kilobyte = 8000 bit
- 10 Mbps = 10,000,000 bit

Bits are the smallest unit of data the '1s' and '0s' and Byte is a basic unit of measurement for storage space, 1 Letter equals 1 Byte.

With a 10Mbps transmission link. 8000 bit / 10,000,000 = .8 miliseconds (Source to Router) + Router to Destination (Assuming R rate is the same for Router to Dest.)  .8 + .8 (Propagation delay = to spread) = .16 miliseconds.

If cut-through method is used it would only take .8 milseconds to S. > R > Dest. since it will not wait for the other packets to arrive.

Assuming that the packet will travel through a series of links with the same transmission rate. (Where **N** is the number of Routers that the packet will pass through and also assume that there is no processing and propagation delay.)
$$ Dend-to-end = N L/R $$ 
Equation 1.1

---

^d0a276
### Queuing Delays and Packet Loss 

Packet switch has an #output_buffer for every attached link, it stores packets that the router is about to send to that link.

The output buffer is place where packets waits if the link is busy with transmission of another packet to the same link.

Arriving or queueing packets are loss if buffer space is full

```ad-example
title: Packet Queue
Host A and B send packets through a 100 Mbps Ethernet link to the router and the router directs packet to the 15 Mbps link if the arrival of packets keeps arriving on the router it will cause an congestion (crowded) in the links **output buffer**. Packet is waited until it is its turn to be transmitted.

![[Pasted image 20220711170555.png]]
```


---

### Forwarding Tables and Routing Protocols
Packet forwarding (transmission) is done in different ways in different types of computer networks.

In the Internet, every end system has an IP address, the sender includes the destination's IP address into the packet's #header.
	
IP address has a hierarchical structure meaning that the router examines a portion of packet's destination address then forwards to the packet to the next router or what they call **Forwarding table**that maps destination address.
	
When a packet arrives the router examines the address and uses the forwarding table to find the right #outbound_link (Outbound = traveling away / in this case it is more like finding the right path to dest.) then router redirects the packet to this outbound link.
	
Internet has a very special #Routing_Protocols that are used to automatically set the forwarding tables to determine the shortest path to configure forwarding tables in the router.
	
```ad-example
title: Forwarding Table
Joe is a driver trying to get to 123 Cancer St in Meyc, sto nino, but he doesn't like to use the map he prefers destination, he asked how to get to the that location to a person, the person extract a portion of the address sto nino, tells joe to go to a specific location in sto nino, joe arrives then asked a person again then person extracts Cancer St then he finall arrived at 123 Cancer St.
```

---


## Circuit Switching
One of the ways to move data across a network.

Resources (buffers, link transmission rate) are reserved for the duration of the communication sessions.

 In packet-switching resources are not reserved therefore there is a big possibility for queue. 

```ad-example
title: Circuit (R-A) vs Packet Switching (R-B)
Restaurant A only accepts reservation, R-B is first come, first serve basis, At R-A, we need to make a call first to make a reservation, but the moment we arrived at the Restaurant we can be seated already but at R-B we dont need to make a reservation we can be immediately seated or worse-case queued.
```

![[Pasted image 20220712100235.png|center]]
														**Figure 1.13**

- Figure 1.13 is interconnected by four links, has four-circuits so it can support four simultaneous connections.

	- If Host A and B wants to communicate with each other the network makes a reservation taking one circuit on each of two links. Circuits are reserved for the duration of the communication.
	
	- If link have transmission rate of 1 Mbps then each end-to-end circuit-switch connection get 250 kbps of guarenteed transmission rate.
	
---

### Multiplexing in Circuit-Switched Networks
- Circuit in link is implemented with *frequency-division multiplexing* or *time-division-multiplexing* 
	
	- **Frequency-division multiplexing**
	    - multiple signals are combined for transmission on a shared medium or link, with each signals have different frequencies
	
		- Frequency band most likely to have a width of 4 kHz (4,000 #hertz or 4,000 cyclers per second) width of band also called #bandwidth

	- #Time-division_multiplexing 
		- Time is divided into frames of fixed duration.
		
		- Posses entire bandwidth of a channel in a fixed duration after that it is the next senders turn.
		
		-  For every frame is divided into a fixed number of time slots

		- Network dedicates one time slot for every frame and the main purpose of those time slots to transmit the connection's data.

 ```ad-example
title: TDM example
In a television serial (a plot that unfolds in order of episodes by episodes)for every 10 minutes of serial is followed by 5 minutes of advertisement.
```

```ad-example
title: TDM and FDM
![[Pasted image 20220714101502.png|center]]
**Figure 1.14**
FDM each circuits have fraction of a bandwidth while TDM gets whole of bandwidth then the next sender posses entire bandwidth.

FDM, frequency domain is segmented into four bands each with a bandwidth of 4 khz

TDM, time domain is segmented into frames with four time slots in each frames
transmission rate is equal to the frame rate multiplied by the number of bits
if a link transmits 8,000 frames per second with each slots consists of 8 bits = 64,000 = 64 kbps

Host A to Host B (file size of 640,000) with all links have transmission rate of 1.536 Mbps = 1536000 bits / 24 bits = 64 kbps | 640,000 / 64 kbps = 10 seconds even if passed through one or one hundred links.
Actual end to end delay includes propagation delay
```

---

## Packet Switching vs Circuit Switching
- **Packet Switching** 
	- A user shares a 1 Mbps link and generates 100 Kbps of data and most of the time the user is 90% inactive (not generating data).
	
	- Probability of a user is active is 0.1 or 10%. 35 users in total that there are 11 or more users simultaneous active is 0.004 #Homework_Problem_P8
	
	- If there are 10 users and only one is active then that user can send packets at its full rate of 1 Mbps. No other users generating packet that needs to be sent on the same link (Multiplexed).
	
- **Circuit Switching**
	- 100 Kbps must be reserved for each user at all times. (Link rate is divided)
	
	- In #Time-division_multiplexing, if one frame is divided into 10 time slots of 100 miliseconds each, making circuit-switched can only support 10 simultaneous users
	
	- 1 Mbps/100 Kbps = 10, one time slot per frame.

	- If more than 10 simultaneously active users, arriving packets are mix together exceeding output capacity of the link. then #output_buffer  will start to grow.
	
```ad-example
title: Time-Division Multiplexing
There are 10 users and one of them generates 1,000-bit packet while the other 9 nine users remain inactive. With 10 slots per frame and each slot consisting of 1,000 bits the active user can only use its one time slot per frame to transmit data. Then the remaining 9 time slot in each frame remain inactive and it will take 10 seconds before all of user'one million of bits of data has been transmitted.
```

---

## A Networks of Networks

End systems connect into the Internet via an access [[NET Computer Networks and the Internet#Internet Service Providers|Internet Service Provider]].

They provide connectivity via #DSL, #cable_modems, FTTH, Wi-fi, and cellular.

To connect billions of end systems the ISPs themselves must be interconnected or like an highway connecting all roads this is done by creating a *network of networks*.

### Network Structure

- Have each ISPs to connect to each other so billions of end systems can be connected.

	- **Network Structure 1**:
		- Interconnect all of the access ISPs with a *single global transit ISP*.
		
		- **Global Transit ISP** have atleast one router near each of the hundreds of thousands of ISPs
		
		- Problem is too expensive and other companies will build their own global transit ISP
	
	- **Network Structure 2**
		- Global transit providers sits at the top tier and access ISPs at the bottom tier.
		
		 - In any given region there may be a **regional ISPs** to which access ISPs in the region connect to.
		 
		 - Then these regional ISPs connects to **tier-1 ISPs** (Similar to our imaginary global transit ISP but they are real) 
		 
		 - There are currenlty dozen of tier-1 ISPs includng Level 3 Communications, AT&T, Sprint, and NTT. 
		
There may be multiple competing tier-1 ISPs but there may be also multiple competing regional ISPs in a region.

Each access #ISPs connects and pays the regional ISPs and regional ISPs pays and connect to Tier-1 ISPs.

```ad-note
title: Access ISPs to Tier-1 ISPs
Access ISPs can directly connect to Tier-1 ISPs.

Tier-1 ISPs doesn't pay anyone since they are at the top of the hierarchy.
```

--- 

## Network Structure 3
In some cases there are regional ISPs that covers a country that the smaller regional ISPs connect to then that larger regional ISPs connect to the Tier-1 ISPs

```ad-example
title: China ISPs
Access ISPs in each city connects to provincial ISPs, which in turn connects to a national ISPs which finally connects to tier-1 ISPs [Tian2012]. This also referred to as multi-tier hierarchy.
```

--- 

```ad-note
title: ISPs
It is also said that access ISPs is a **customer** and the one which it connects to wether it is a regional ISP or tier-1 ISPs is the **provider** same priniciple in regional and tier-1 ISPs
```

---

### Network Structure 4
A network that is more closely resembles today's Internet with **points of presence**, **multi-homing**, **peering**, and **Internet exchange points** into the hierarchical Network Structure 3.

- **POP**
	- Exists all levels of the hierarchy except the bottom tier (access ISPs)
	
	-  A group of one or more routers at the same location where customer ISPs connect to into the provider ISP (The 'a group of one or more routers.').
	
	- A provider's pop rent a high-speed link from a third-party telco provider to one of its customer network to directly connect one of its routers to a router at the Pop.

- **Multi-Home** 
	- Any ISP can multi-home (except for tier-1 since they are at the top level) or to connect to two or more provider ISPs

```ad-example
title: Multi-home
An access ISPs can multi-home with two regional ISPs, or it may multi-home with two regional ISPs and one tier-1 ISP and regional ISPs can multi-home with multiple tier-1 ISPs
```

When an ISP multi-home even if one of the providers has a failure it can continue to send and receive packets into the Internet.

The fee depends on how much traffic the customer ISP exchanges with the provider ISP.

- **Peer**
	- To reduce the cost of how much the customer ISP pays to the provider
	
	-  A pair of ISPs at the same hiearachy level can peer or they can directly connect their networks together so that all of traffic passes between them passes over to the direct connection.
	
	-  Settlement is free, neither ISPs does't need to pay each other.

- **Internet Exchange Point**
	- Usually a stand-alone building with its own switches created by a third-party company.
	
	- Is a meeting point where multiple ISPs can peer together.

---

## Network Structure 5
The today's Internet.

Network Structure 5 is built on top of Network Structur 4 by adding **content-provider networks**

**Google** is the leading example of content-provider network as Google have 19 major data centers across almost all part of the world serving billions of data.

Smaller data centers that belongs with Google have a few hundred serves and they are often located within IXPs

Google data centers are interconnected via Google's private TCP/IP network but it is not entirely seperated from the public Internet.

Google's private network only carries traffic from/to Google servers.

Google attempts to bypass the upper tiers by connecting lower ISPs directly to Google's private network or through IXP.

Most access ISPs can still only be reached by carrying through tier-1 networks.

Google's network also connects to tier-1 ISPs and pays them for the traffic it exchanges with them.

The advantages of this is Google pay less by having their own network and have greater control of how they will serve their content to the end users.

![[Pasted image 20220718132051.png|center]]
**Figure 1.15**

More on [[Google's Network Infrastructure]].

---

References:
[[NET Computer Networks and the Internet|Computer Networks and the Internet]]
