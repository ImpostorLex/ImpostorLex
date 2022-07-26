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

It is similar to finding a treasure, a person who wants to hide the treasure goes to a place(routers), leaving clues (messages, name and address) for the hunter(special packet) until the hunter reaches the X spot or (the final destination)