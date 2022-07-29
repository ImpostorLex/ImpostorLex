```toc
```

Up:: [[NET Delay, Loss, and Throughput In Packet Switched Networks]]
Tags:: #on/QueueDelay #on/PacketLoss 
Date:: 07/29/2022

---
# Queuing Delay and Packet Loss

Is so important that there are thousand of books written about it.

It differs from packet to packet's size or amount.

```ad-example
If 10 packet arrives at an empty queue at the same time, the first packet will suffer no delay while the last suffer will suffer great delay from first 9 packets.
```

Often time statistical measures is needed such as average, variance, and the probability of queuing delay with a given value.

It all depends on the arrival rate of packets and the transmission rate of the link.

#La/R
*a* = the average rate of packet arriving at the queue (units of packets/sec).
R = is the transmission rate (in bits/secs or bits per second).
L = Number of bits inside a packet.
$$ La/R $$
 Is called **traffic intensity**.
$$ La/R > 1 $$
The queue is overloaded and it won't stop.
$$ La/R\le 1 $$
If packet arrives from time time then packets will not experience queuing delay.

In the real world, there is no pattern for arrivals of packet, they arrive in random amount of time.

---

## Packet Loss

Routers queuing capacity depends on the cost and design.

Packet delay dont approach infinity since links have limited capacity.

If queuing is full, all arriving packets will be dropped or lost.

Lost packets can or may be re-transmitted on an end to end basis.



---

Some Info about Queuing Delay [[NET Network Core#^d0a276|here]] and Store-and-Forward [[NET Network Core#^b46806|here]].

Continues here at [[NET End-To-End Delay|End-To-End Delay]].
[[Networing MOC]]