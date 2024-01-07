Upper layer protocols that use service from the network layer expect to get an ideal service. But the network layer is not perfect.
We can measure the performance of the network layer in terms of:
* Delay
* Throughput
* Packet loss
You can improve the performance by congestion control

***
#### Delay
Anyone who has tried to use a network knows that there is a certain delay in the response you get from the network. This delay consists of four components:
![[Pasted image 20231011215101.png]]

***
#### Throughput
Throughput is defined as the number of bits that pass a given point in the network per second.
A packet that follows a route from sender to receiver will typically pass several links (networks) with different transmission speeds.
![[Pasted image 20231011215136.png]]

However, the actual situation on the Internet is that the data normally passes through two access networks and the Internet backbone.
![[Pasted image 20231011215227.png]]

You may also find that several hosts have to share links on some routes.
![[Pasted image 20231011215256.png]]

***
#### Packege Loss
Package loss has a serious effect on the performance that can be achieved.
Although a router has buffers to store packets while others are being
processed, these buffers have only limited sizes.
If they are filled up completely, then it can lead to loss of packets because the coming packets will be dropped!
This means that lost packets must be re-transmitted, which can lead to even worse data traffic and thus loss of even more packets.

***
#### Congestion control
[[Network Congestion control|congestion control]] is a mechanism that should help increase the performance.
Although the Internet model does not directly address this issue on the network layer, but more on the transport layer (which we will see later).
A study of congestion at the network layer may help us to better understand the cause of congestion at the transport layer and find possible remedies to be used at the network layer.
![[Pasted image 20231011215529.png]]

Two categories of control techniques:
* Open-loop congestion control (prevention = before the problem occurs)
* Closed-loop congestion control (removal = after the problem has occurred)

***
##### Open-loopcongestion control
**Retransmission policy:** Retransmission cannot always be avoided. Here it is the sender who starts a timer.
If the timer expires before the sender has confirmed that the packet has arrived, it is retransmitted. (we have also seen this at the Data Link layer level)
It is important that the retransmission timer is optimized so that an answer has a reasonable time for reaching. But, also not for too short time as this may increase the congestion and worsen efficiency.
We remember that too much retransmission increases the load on the network.

**Window policy:** The types of windows (buffer space) used by the sender also affect the load in the system.
Selective Repeat Window is better than **Go-Back-N Window** in relation to the load 
* **Selective Repeat Window** retransmits only missing packets. It is the receiver’s responsibility to put them in order when they arrive.

* **Go-Back-N Window** retransmits all packets from a missing packet.
The receiver does not need to be able to put them in order, as it will always receive the packet in order (if they do not come in order, the recipient asks to get them back from where the loss occurred)
requires larger buffer at the sender.

**Acknowledgement policy:** If the sender is receipt-controlled by the receiver, then a proper frequency of the [[Flow and error control#ACK|ACK]] can help regulate the load.
The receiver can also just send a receipt for N packets. Because we remember that [[Flow and error control#ACK|ACK]] packages are also considered as loads in the system.
This policy seems familiar! This corresponds to flow and error control at the Data Link layer level.

**Discarding policy:** Here it is the router that discards packets.
A good policy here can prevent congestion without harming the integrity of the transmission. An example here could be audio transmission, if you could discard less sensitive packets then congestion could be avoided without significantly affecting the sound quality.

**Admission policy:** this policy is linked to a QoS (quality-of-service)
mechanism, which we will not go into in more detail in this course.
But it is equivalent to applying for a permit for a free link through the Internet, i.e., allocating resources (port reservation) in all routers/switches on the path "a kind of green channel", so that in principle you get an available point-to-point connection between sender and receiver.

***
#### Closed-loop Congestion Control
Backpressure is a technique in which a congested router stops receiving packets from its upstream node or nodes.
![[Pasted image 20231012102053.png]]
Note that this technique can only be used for connection-oriented data traffic, where the routers know where the traffic comes from.
>This is a bit like cars stopping in a queue

**Choke Packet:** a Choke Packet is a special data packet sent directly from a congested router to the sender (source) to inform of the congestion.
As we will see later in the course, the ICMP (Internet Control Message Protocol) protocol is used.
* Here, a router finds that it is being overwhelmed with IP datagrams.
* It discards some of them.
* And notifies the sender directly here via ICMP.
* The intermediate routers (I and II in the figure) do not get notified.
![[Pasted image 20231012102232.png]]

**Implicit signaling:** In implicit signaling, there is no communication between the congested node or nodes and the source.
If a sender (source) detects that it takes too long before a [[Flow and error control#ACK|ACK]] receipt is received, then it can interpret it as an overload problem and slow down sending packets.
Explicit signaling: A router that experiences an overload can explicitly send a signal to the sender or receiver.
This method differs from the Choke packet method, where a separate packet was sent.
(e.g., ICMP packet) Here, the signal is included in the packets that carry data (and thus not in another protocol).

>This type of congestion control is often seen in ATM (Asynchronous Transmit Mode) networks, i.e., long-distance networks.
