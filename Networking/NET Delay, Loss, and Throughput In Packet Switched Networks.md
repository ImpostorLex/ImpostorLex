
[[Networing MOC]]
# Delay, Loss, And Throughput

The Internet can be viewed as an infrastructure that provides services to #Distributed_applications running on end systems.

Computer network limits the [[NET Terms#^70e203|throughput]] between end systems

## 1.4.1 Delay in Packet-Switched Networks
Packet starts from the source and it passes through a series of routers and the journey end when it reaches the destination.

Everytime the packet travels through a node (routers, host) to another node it suffers from types of delay at each node.

These are **nodal processing**, **queueing delay**, **transmission**, and **propagation delay** and they combine and form a **total nodal delay** they affect many Internet applications by these network delays.

---

### Types of Delay

On **Figure 1.16**, a packet sent through the upstream node from Router A (has an #outbound_link ) to Router B. 

The links comes in order by queue known as buffer. When a packet arrives at Router A the router examines the packet's header and determine the appropriate outbound link then directs the packet to that link, if there is no currently packets that is being transmitted if so the packet will be queued and waits for its turn.

![[Pasted image 20220719104950.png]]
**Figure 1.16**

---

### Processing Delay
The time required to examine the packet's header and determine where to direct the packet and the checking for bit-level errors on packet's that is transmitted from upstream node (In **Figure 1.16** case, upstream node to Router A)

Delay are usually in miliseconds.

---

### Queueing Delay
Length of queuing delay depends on packets that arrive earlier than our packet that are queued for transmission since the link is currently busy transmitting a packet (Queuing delay is *zero* if there are currenlty no queue and transmitting packets).

Delay are usually in microseconds to miliseconds.

---

### Transmission Delay
Packet switched networks is a *first-come-first-served manner*.

Our specific packet will only be transmitted once all packet before us is transmitted. 

Packet length is denoted (sign) *L* and transmission rate of the link (In **Figure 1.16** router A to B) is denoted by *R* in bits/secs

```ad-example
title: *R* transmission rate
With an Ethernet link rate of 10 Mbps then our *R* = 100 Mbps and Packet length in bits is 12000 bits.

$$t=12000/100\times10^6 = 0.12ms $$

$100\times10^6$ = 100,000,000 bits since calculation is always in bits (100 Mbps)

So it wall take 0.12ms to transmit or push the packets to Router B
```


---
References:
[[NET Network Core#^17c2e0|Packet Switching]]
