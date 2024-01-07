The network layer in version 4 can be thought of as one main protocol and three auxiliary ones.
![[Pasted image 20231024130251.png]]
**IPv4** is responsible for packetizing, forwarding, and delivery of a packet at the network layer.

**Internet Control Message Protocol version 4 (ICMPv4)** helps IPv4 to handle some errors that may occur in the network-layer delivery.

**Internet Group Management Protocol (IGMP)** is used to help IPv4 in multicasting.

**Address Resolution Protocol (ARP)** is used to glue the network and data-link layers in mapping network-layer addresses to link-layer addresses.

***
IPv4 is an unreliable and connectionless datagram protocol - a best-effort delivery service.
The term best-effort means that IPv4 does not offer any flow and error control, and that packets can be corrupted, be lost, arrive out of order, or be delayed, and may create congestion for the network (however, error detection on the header).
IPv4 recognizes the unreliability of the lower layers and does its best to get its transmission to the receiver, but without any kind of guarantee.
If reliability is important, then IPv4 must be paired with a reliable transport layer protocol e.g., TCP.
* Datagrams are used and each datagram is handled independently.
* This means that they do not necessarily follow the same path and therefore may arrive out-of-order at the receiver.
* Packets may also be damaged or lost. But IPv4 relies on the higher-level protocols to take care of these problems.

***
#### Internet Protocol IPv4 – Header format
![[Pasted image 20231024130612.png]]

The header is 20 to 60 bytes in length and contains information essential to routing and delivery.
* **Version (Ver):** is a 4-bit field that defines the version of the IPv4 protocol, which obviously has the value of 4. This field tells the IPv4 software that all fields in datagrams must be interpreted as specified in the IPv4 protocol.
* **Header length (HLEN):** is a 4-bit field that indicates the total length of the datagram header in 4-byte words.
This field is necessary as the header can have a variable size.
If there are no options, then the header takes up 20 bytes, and the value of HLEN will thus be 5 (5 x 4 bytes = 20 bytes).

* Service: This field has had both name and interpretation changed. The field is 8 bits and was previously called Service type, now it is called differentiated service.
The field is used to distinguish and prioritize data transmission in case
of congestion.

***
![[Pasted image 20231024130841.png]]
* **Service type** (former meaning)
In this implementation, the 3 MSBs (bits) are called Precedence bits, the next 4 bits are called type of service (TOS) and the last bit is not used.
a) **Precedence:** This 3 bit subfield defines the priority of the datagram in case of congestion (traffic).
If a router p.g.a. congestion has to discard datagrams, then it will be the ones with the lowest priority.
Datagrams used for e.g., network management, are more important than other datagrams.

b) **TOS bits:** This 4-bit subfield has a special meaning, note that only
one bit at a time can be 1.

* Interactive activities, activities that require immediate attention and activities that require quick response must have a minimum delay.
* Activities that send a lot of data must have maximum throughput.
* Management activities must have maximum reliability.
* Background activities must have a minimum cost.

***
![[Pasted image 20231024131055.png]]
* differentiated service (current meaning) In this implementation, the 6 MSB (bits) form a subfield called codepoint, the last two bits are not used.

a) When the 3 LSBs (bits) are all 0, then the 3 MSBs (bits) are interpreted in the same way as in the Percedence subfield in the Service Type implementation.

b)When the 3 LSBs (bits) are not all 0, the 6 bits define 64 different service types, based on their priority. Category 1 contains 32 service types, Categories 2 and 3 contain 16 service types. The priority of these types of services is determined by the IETF (Internet Engineering Task Force)

***
• **Total Length:** This field is 16 bits and indicates the total length of the datagram (both header and data).
Since this field in IPv4 is 16 bits, the length of the datagram is limited to 65,535 (216-1) bytes, from which 20 to 60 bytes must be subtracted because of the header.
The rest is data from the upper layer. If the length of a datagram becomes less than the minimum length of the protocol used on the Data Link layer e.g., Ethernet, then fills up with padding ("Data < 46 bytes" corresponds to the Datagram).
![[Pasted image 20231024131209.png]]

***
* Identification: This field is used in connection with fragmentation (we will see later).
* Flags: This field is used in connection with fragmentation (we will see later).
* Fragmentation offset: This field is used in connection with fragmentation (we will see later).
* Time to Live: A datagram has a limited lifetime when transmitted around the Internet to avoid circulating on the Internet forever. This value is approximately two times the maximum number of routers between any two hosts. Each router that processes the datagram decrements this number by one. If this value, after being decremented, is zero, the router discards the datagram.

***
* Protocol: This 8-bit field indicates which protocol the payload (packet) carried by the IPv4 datagram comes from. An IPv4 datagram can encapsulate data from many different protocols, e.g., [[TCP (Transmission Control Protocol)|TCP]], [[UDP (User Datagram Protocol)|UDP]], [[ICMPv4]] and IGMP. The field indicates who is the final receiver of the data that the IPv4 datagram provides, and thus which protocol the data belongs to.
![[Pasted image 20231024131354.png]]

![[Pasted image 20231024131420.png]]

***
* Checksum: We will look at the Checksum concept and its calculation later.
* Source Address: The sender address is a 32-bit field that indicates the sender. This field must remain unchanged throughout the transmission through the Internet from sender to receiver.
* Destination address: the receiver address is a 32-bit field that indicates the receiver. This field must remain unchanged throughout the transmission through the Internet from sender to receiver.

***
#### Option Section
The fixed part of the header is 20 bytes. In addition, we have a variable part of 40 bytes, which we call option section.
![[Pasted image 20231024133716.png]]
Options are divided into two broad categories: single-byte options and multiple-byte options.

* No Operation: this is a 1-byte option used as a filler between options.
* End of Option: this is a 1-byte option used for padding at the end of the option field. It can only be used as the last option.
* Record Route: A record route option is used to record the Internet routers that handle the datagram. It can list up to nine router addresses. It can be used for debugging and management purposes.

* Strict Source Route: This option is used by the sender to predetermine the route that a datagram should take through the Internet.

This selection of the route by the senders can have several purposes: o The sender can select a route with specific services, such as minimum delay or maximum throughput. o The sender can choose a route that is safer and more reliable. E.g., you can choose a route so that you do not use the competitors' networks. 

If the sender specifies a specific route, then all routers mentioned in this option must be visited.

A router must not be visited if it is not mentioned in this option. If a datagram visits a router that is not in the list, it is discarded. If a datagram has not visited all the routers in the list when one arrives at the receiver, it will also be discarded.

* Loose Source Route: This option is similar to the Strict Source Route but is less strict. All routers in the list must be visited, but other routers can also be visited.
* Timestamp: A timestamp option is used to record the time of datagram processed by a router. The time is expressed in milliseconds from midnight, Universal time or Greenwich mean time. Knowing the time when a datagram is processed can help users and managers track the behavior of the routers in the Internet. We can estimate the time it takes for a datagram to go from one router to another.

