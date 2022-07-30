Up:: [[NET Queuing Delay and Packet Loss]]
Tags:: #on/End-to-End #on/Delay 
Date:: 07/29/2022

---

# End-To-End Delay

Total delay from source to destination

```ad-example
title: End-to-End Delay
Suppose all, *N* - 1 routers between source and destination, no traffic, processing delay in source host and each router is *dproc*, and the transmission rate of each router and source host is R bits per second, and laslty propagation delay is *dprop*

$$ d_end-end = N ( d_proc + d_trans + d_prop) $$

Equation (1.2)

Given: 
$$Propagation Speed:- 2.5\times10^8 m/s $$

$$ Link Speed:- 2 Mbps $$

$$ Routers:- 2$$

Packet Size:- 1500 Byte

![[Pasted image 20220726111231.png]]

**Tranmission Delay for Segment 1**

ES1 pushes the packet to the wire (Chef just told waiter to pick up food)

**Note: Calculation always in Bits**

$$ {L/R} = 1500 B / 2 Mbps = 6 Ms $$

**Propagation Delay for Segment 1**

Once packet hit the wire and how long would it take to make it to router 1 (waiter picks up food on going to customer with time.)

$$ {D/S} = 5000 km / 2.5 x 10^8ms = 20 Ms $$

**Tranmission / Segment 2**

Same as segment 1 since given still the same.

**Prop / Segment 2**

$$ {D/S} = 4000 km / 2.5 x 10^8ms = 16 Ms $$

**Segment 3**

**Transmission**

Same as segment 1 since given still the same.

**Propagation**

$$ {D/S} = 1000 km / 2.5 x 10^8ms = 4 Ms $$

And laslty processing delay for every packet that passes through each router is 5 ms

Total End-to-End delay:

Segment 1 = 26 ms
Segment 2 = 22 ms
Segment 3 = 10 ms
Router Processing = 10 ms
Total = 68 ms

Reference:- [here](https://madpackets.com/2020/05/01/calculate-end-to-end-delay/)

```

---

## Traceroute
Is a tool to see or measure the end-to-end delay in a computer network.

User need to specify the destination hostname, in the source, the program sends a special packets to the destination as they passes a series of routers, the special packets that passes a series of router sends back a message containing the name and address of the router.

```ad-example
title: Traceroute.
Suppose there are four routers form source to destination.
Source will send 3 special packets to first hop router, then router sends back reply in miliseconds per packet including name and address of the router back to traceroute(source), then traceroute again sends 3 packets to the next hop router and does the same to the third router, each of these packets are marked *n*.

First packet sent is number 1 and so on.
![[Pasted image 20220728111953.png]]

Example of message returned to source:
**1. gw-vlan-2451.cs.umass.edu (128.119.245.1) 1.899 ms 3.266 ms 3.280 ms**

**1** =- No. of router
**gw-vlan-2451...** =- name of the router
**(xxx.xxx.xxx.xxx)** =- address of the router.
***** :- In place of **ms** columns if special packet is dropped.

**Note:- These delays include all types of delay discussed.**

Wherein the last three columns are the Round-Trip Delay, packets send and returned back to source message in elapse time.
```

---

### End System, Application, and Other Delays

Aside from [[NET Delay, Loss, and Throughput In Packet Switched Networks#Types of Delay|different types of delay]], there are some significant additional delays.

```ad-example
title: Transmission delay protocol in a shared medium
Such as Wi-fi or cable modem when an end system wants to send a packet into the shared medium it may purposefully delay the transmission because as part of its protocol for sharing a medium.
```

```ad-example
title: Media packetization delay
It is present in Voice over-IP or VoIP, these are skype, and whatsapp, the sender side will fill a packet that is in encoded digitized speech before passing the packet to the Internet.
```

---

Down: [[NET Throughput in Computer Networks]]
[[Networing MOC| Map of Content]].