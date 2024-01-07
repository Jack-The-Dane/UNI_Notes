There are many tools that can be used for troubleshooting on the Internet. We can follow the route for packets, we can examine many different host and router types and so on.
But here we will look in particular at two tools:
* Ping
* Traceroute

***
#### Ping
The ping program can be used to determine if a host is alive and is able to respond.
We use the Ping program here to see how it uses ICMP packets.
* The sender sends an ICMP echo request (type = 8 and code = 0)
* The receiver responds with an ICMP echo reply if it is alive
* The ping program now sets the identifier field in the echo request and echo reply messages. (so that you know which messages belong to the sequence)
* The ping program starts the sequence number from 0 and this number is increased by 1 each time a new message is sent.
* The ping program can calculate Round-Trip-Time (RTT). It insert the sending time in the data section of the message. When the message arrives, it subtract the departure time from the arrival time to get RTT.
![[Pasted image 20231024135729.png]]
The [[HOP and TTL#What is TTL(Time to Live)|time to live (TTL)]] in the IP header in this example is 62, which means that the datagram can visit up to 62 [[HOP and TTL#What is a hop|hops]] before it is discarded. 

The [[Debuggin tools#Ping|pings]] program tells you that there are 56 bytes of data out of 84 bytes (total). This corresponds to the IP datagram
IP header (20 byte) + ICMP header (8byte) + data (56 byte) = total (84 byte).
Note: each row says 64 bytes! This corresponds to the ICMP package
ICMP header (8byte) + data (56 byte) = 64 byte

***
#### Traceroute
This program can be used to trace the path of a packet from a source to the destination.
The program is called:
* Traceroute in UNIX
* Tracert in Windows

The program conveniently uses two ICMP error-reporting messages to figure out the path:
* Type11: Time Exceeded
* Type3: DestinationUnreachable
The program is an application layer program and uses [[UDP (User Datagram Protocol)|UDP]] as transport layer protocol.

The program is an application layer program and uses [[UDP (User Datagram Protocol)|UDP]] as transport layer protocol.
![[Pasted image 20231024135858.png]]

1. The traceroute program uses the following procedure to find the IP address of the first router and the round-trip time between the sender and the first router.

a. The traceroute program on the sender uses [[UDP (User Datagram Protocol)|UDP]] to send a packet to the receiver host. The message is encapsulated in an IP datagram with the value in the time-to- live field set to 1. The program records the departure time of the packet.

b. The first router receives the packet and counts down the TTL value so that the value becomes 0. The packet is discarded for this reason and an ICMP Time Exceeded message is sent back to the sender.

c. The traceroute program on the sender receives this ICMP error message, from which the IP address of the first router can be found from the source IP address of the error message.
The program also record the arrival time. The difference between this time and the departure time from step a is the round-trip time. The program repeats steps a-c three times to obtain a better average round-trip time.

>The first time takes longer as ARP has to look up in its table, the second and third time uses the physical address stored in the cache.

2. The traceroute program repeats steps a to c (in step 1) to find the IP address and round-trip time of another router. The value in the TTL field is increased by 1 every time (e.g., 2 for the second router, and 3 for the third router).

3. The traceroute program repeats step 2 until the IP address and round-trip time of the receiver host are found. For the sender host to know that the packet has finally reached the receiver host, the traceroute program use UDP packets:

* The program has set a port value in the [[UDP (User Datagram Protocol)|UDP]] header that does not exist.
* When the receiver host receives the packet, it cannot find the specified port number in any application layer programs.
* The receiver host therefore sends an ICMP message of the type "The recipient cannot be reached" back to the sender host (Type3: Destination Unreachable, code: 3)

>Note that nothing like this happens when the UDP packet arrives at the routers as routers do not check the UDP header.

![[Pasted image 20231024140434.png]]

***
#### ICMP Checksum
The Checksum is calculated for the entire message, i.e., both header and data section.
* The checksum field is initially set to 0
* The message is divided into 16-bit sections, which are added together
* The sum is complemented (reversed bit by bit)
* The result is inserted in the Checksum field.
![[Pasted image 20231024140515.png]]
