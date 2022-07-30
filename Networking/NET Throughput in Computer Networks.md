Up:: [[NET End-To-End Delay]]
Tags:: #on/Delay #on/Throughput 
Date:: 07/29/2022

---

# Throughput in Computer Networks

Is another **factor** for performance in a computer network.

It is the amount of **data** that is moved succesfuly from one place to another.

It is measured in **bits/sec**, wherein  *F* indicates the **bits** and *T* indicates the **seconds**.

```ad-example
title: Host A to Host B file transfer
A large file measured in **10,000 bits** and it takes 8 **seconds** for host B to receive all *F* bits then the **average throughput** is 10,000 bits per 8 seconds.
```

---

## Important Concept of Throughput

![[Pasted image 20220730110355.png]]
**Figure 1.19**

%% On fig A %%
Two end systems, a server and a client, connected by [[NET Computer Networks and the Internet#Communication Links|communication links]] and a router.

Let **Rs** denote the rate of link server to router and Let **Rc** denote the rate of router to client.

We may think of **bits** as *fluids* wherein the **links** are *pipes*.

Since **communication links** have a **transmission rate**, it clearly show that the server cannot pump bits through the link that is greater than **Rs** and the same goes for router, it cannot forward bits if its greater than the **Rc**.

if **Rs** is less than **Rc** then the bits will have no problem transmitting data to **client** (Giving the throughput of **Rs**).

If **Rc** is less than **Rs** then the router will not quickly forward the bits (Giving the throughput of **Rc**).

```ad-example
title: *F/min{Rs,Rc}*
**NOTE:-** MBPS - Megabits per second not megabytes. 1 Mbps = 1000000
File size:- 32 million bits
**Rs**:- 2 Mbps
**Rc**:- 1 Mbps

$$ 32,000,000 / 1000000 = 32 $$

It will take a total of **32 seconds** to download the file from server to client.
```

This is without the [[NET Network Core#Store-and-Forward Transmission|store-and-forward]] and **processing delays**.

---

On **Figure 1.19(b)**

Shows a network with *N* links between the server and receiver and the transmission rate of each link is indicated **Rn**.


---

Down:: [[]]
[[Networing MOC]].
