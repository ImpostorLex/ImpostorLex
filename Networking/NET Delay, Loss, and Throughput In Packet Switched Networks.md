
[[Networing MOC]]
# Delay, Loss, And Throughput

The Internet can be viewed as an infrastructure that provides services to #Distributed_applications running on end systems.

Computer network limits the [[NET Terms#^4e7949|throughput]] between end systems.

---

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

```ad-note
title: Packet Queueing Delay
**a**:- Average packet arrival rate
**L**:- Packet Length (bits)
**R**:- Bandwidth (Bit transmission rate)
$$L\times a/R$$

![[Pasted image 20220721124445.png]]
```

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

### Propagation Delay

^ed4547

Is the time required to continue from the beginning of the link to router B.

Distance between the two routers.

Propagation depends on the [[NET Computer Networks and the Internet#Communication Links|Physical Medium]] of the link and have a range of

Length of the link.

$$2\times10^8 meter/sec - 3\times10^8 meters/sec$$

Almost equal to the speed of light.

It is the distance between two routers divided by the propagation speed.

*D* represents the distance between the routers A and B and *S* is the propagation speed of the link. 

$$ d/s $$

---

### Transmission and Propagation Delay

Transmission delay is the time required to push out the packets.

Propagation delay is the time it takes for a bit to spread/cross from one router to another (until it gets to its destination).


**Figure 1.17**

```ad-example
title: Transmission and Propagation

A highway(The **link**) that have a toolbooths(The **Routers**) for every 100 kilometers and a car that travel(**propagate**) on **highway** with a speed of 100 km/hour (everytime a car leaves a toolbooth it have the speed of 100 km/hour instantly) and the next 10 cars(The **bits**) follows each other in a fixed order and the #caravan as packet and tollbooth services(**transmits**) has a rate of 12 seconds per car.

![[Pasted image 20220720104100.png]]

Say that if one car of the caravan arrives first at the toolbooth, it waits for the entire 9 cars lined up behind it in other words entire caravan must be stored at the toolbooth first before it can get forwarded([[NET Network Core#Store-and-Forward Transmission|Store and Forward]]).

So for a toolbooth to push the entire caravan into the **highway** would take 
for a toolbooth to process 5 cars (12 seconds each) = 1 minute, for a toolbooth to process 10 cars would take 2 mins that is the **transmission delay**.

And the time for a car to travel from exit toolbooth to the next is 1 hour because the link speed (or the highway) have a speed of 100 km/hour and the next toolbooth location is in 100 km so it would take an hour to get one car from one exit toolbooth to the next is the **propagation delay**. In total of 62 minutes.
```

```ad-seealso
title: Much Faster, Transmission and Propagation
Car travels(**propagate**) at the rate of 1,000 km/hour and tollbooth services per car is minute, Total time to serve all ten cars in a tollbooth will be **10 minutes** and travelling between two tollbooths is **6 minutes**, since 100 % 1000 = 0.1 x 60(Mins in seconds) = 6 mins.
```

```ad-example
title: Transmission vs Propagation
**Transmission Delay:**
In a restaurant before we get the food the chef/cook have to prepare it and cook it first because you can't serve raw food to people.

**Propagation Delay:**
When the food is ready to serve how much time will the food get to its customer, that depends on the distance of the customer and how fast the waiter is (think of waiters as the links).
```

---

#### Total Delay

$$ Dnodal = Dproc + Dqueue + dtrans + dprop $$

Contribution of each delay sometimes is only small amount barely noticed.

For example *Dproc* can be just microseconds if two routers are only in the same university, it is often negligible but it influences the router's maximum #throughput .

Next is *Dtrans* can be small amount to noticeable, if the transmission rate is 10 Mbps it is not noticeable, however if a packet is sent over the Internet witth slow modem links it can be noticeable.

```ad-note
Nodal delay only talks about the delay at a single router.

End-to-End delay talks about the total delay from source to destination [[NET End-To-End Delay|End-to-End Dela]].
```

---
References:
[[NET Network Core#^17c2e0|Packet Switching]]
