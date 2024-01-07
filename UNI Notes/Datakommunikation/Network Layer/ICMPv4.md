As we have seen before, IP protocol delivers an unreliable and connectionless datagram.

The IP protocol has no error-reporting or any error-correcting mechanism.
* What happens if a router has to discard a datagram because it cannot find a router to the final destination?
* What happens if the time-to-live field reaches the value 0?
* What happens if the final destination host must discard the received fragments of a datagram because it has not received all fragments within a predetermined time limit?

The IP protocol also lacks a mechanism for management queries:
* A host sometimes needs to determine if another host or a router is alive or not.
* Sometimes a network manager needs information from another host or router.

> Internet Control Message Protocol (ICMP) is designed to compensate for these issues. One can consider ICMP as a companion to the IP protocol.

***
#### Message Types
ICMP messages are divided into two broad categories:
* Error-reporting messages.
* Query messages.

**Error-reporting messages:** report problems that a router or a host (destination) may encounter when it processes an IP packet.

**Query messages:** help a host or a network manager get specific information from a router or another host. Some examples:
* Nodes can detect and discover their neighbors.
* Hosts can get information about routers found on their network.
* Routers can help a node redirect its messages

![[Pasted image 20231024134556.png]]
**Type:** The 1-byte field indicates the ICMP type.
**Code:** The 1-byte code field specifies the reason for the particular message type. 
**Checksum:** This last 2-byte field indicates the checksum
**The rest of the header:** is specific to each message type.

***
#### Error Reporting
* ICMP is partially designed to compensate for IP deficiencies.
* But ICMP does not correct errors, it simply report them.
* Error correction is left to protocols on the upper layer.
* Error messages are always sent to the original source because the only information available in the datagram about the route is the source and destination IP addresses.
![[Pasted image 20231024134736.png]]

![[Pasted image 20231024134746.png]]

***
One should be aware that all ICMP error messages contain a data section that contains: **The IP header and the first 8 bytes of the IP data section.**

**The IP header is included** because it contains the sender address to which the error message is sent.

**The 8 bytes of data are included** because the first 8 bytes provide information about the port numbers ([[UDP (User Datagram Protocol)|UDP]] and [[TCP (Transmission Control Protocol)|TCP]]) and sequence number (TCP). This information is needed so the source can inform the protocols (TCP or UDP) about the error.

ICMP forms an error packet, which is then encapsulated in an IP datagram.
![[Pasted image 20231024134858.png]]

***
![[Pasted image 20231024135012.png|200]]
**Type3: Destination Unreachable:** this message uses different codes (0 to 15) to define the type of error message and the reason why a datagram has not reached its final destination. For example, code 0 tells the source that a host is unreachable. This may happen, for example, when we use the HTTP protocol to access a web page, but the server is down.

***
![[Pasted image 20231024135046.png|200]]
Type4: Source Quench: this message informs the sender that the network has encountered congestion and the datagram has been dropped. The source needs to slow down sending more datagrams. In other words, ICMP adds a kind of congestion control mechanism to the IP protocol by using this type of message. 

***
![[Pasted image 20231024135123.png|200]]
Type5: Redirection: this message is used when the source uses a wrong router to send out its message. The router redirects the message to the appropriate router but informs the source that it needs to change its default router in the future. The IP address of the default router is sent in the message. 

***
![[Pasted image 20231024135215.png|200]]
Type11: Time Exceeded: this message can be generated for two reasons:
1. As we have seen before, the IP datagram has a [[HOP and TTL#What is TTL(Time to Live)|time-to-live (TTL)]]  field that is counted down by 1 each time it passes a router. If a router finds that this value has become 0 after such a countdown, then a message is sent back to the sender.
2. The time-exceeded message can also be sent when not all fragments of a datagram arrive within a predefined period of time.

***
![[Pasted image 20231024135241.png|200]]
Type12: Parameter problems: Every ambiguity in a datagram's header can create serious problems as it travels through the Internet. If a router on the way or the receiver detects missing values in any fields in the header, or some options can not be interpreted, then the datagram is discarded, and a message is sent back to the sender. 