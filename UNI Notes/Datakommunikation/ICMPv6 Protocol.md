ICMP has been modified in version 6 as well. This new version, Internet Control Message
Protocol version 6 (ICMPv6), follows the same strategy and purposes of version 4.
The ARP , ICMP and IGMP protocols in version 4 have been merged into ICMPv6.
ICMPv6 performs error reporting and diagnostic functions.
![[Pasted image 20231031130428.png]]

## Messages
![[Pasted image 20231031131422.png]]
### Error messages
ICMPv6 forms an error packet, which is encapsulated in an IPv6 datagram and sent back
to the original sender of the failed datagram.

• Destination-Unreachable message: same as in version 4. There is no protocol on the
receiver that will receive the datagram, therefore a host cannot deliver the content of
the datagram to the upper layer protocol.

• Packed-Too-Big message: new in version 6. If a router receives a packet larger than its
MTU (Max. Transfer unit), the packet is discarded and an ICMP message is sent back to
the sender (packet too large).

• Time-Exceeded message: same as in version 4. Either if the time-to-live counter
reaches zero or if not all fragments of a datagram have arrived on time.

• Parameter-problem message: same as in version 4. used when a router or the
destination host discovers any ambiguous or missing value in any field of the header.

### Informational messages
Here are two informative messages:
• Echo-request: same as in IPv4
• Echo-reply: same as in IPv4
The echo-request and echo-reply messages are designed to check whether two devices on
the Internet can communicate with each other.

### Neighbor discovery messages
Two new ND (Neighbor-Discovery) and IND (Inverse Neighbor-Discovery protocols clearly
define the functionality of these group messages. The two protocols are used for three
purposes:
1. Hosts use the ND protocol to find routers in the neighborhood that will forward
	packets for them.
2. Nodes use the ND protocol to find the link-layer addresses of neighbors (nodes
	attached to the same network).
3. Nodes use the IND protocol to find the IPv6 addresses of neighbors.

Other Neighbor discovery messages:
**Router-Solicitation message**
A host finds a router in the network that can forward IPv6 datagram. (same as in IPv4)

**Router-Advertisement message**
It is a response to a router solicitation message.

**Neighbor-Solicitation message**
In version 6, the ARP protocol is eliminated. This functionality (acquire the MAC address
by knowing the IP address) is now part of ICMPv6, and can be implemented by this type
of messages. (now there is a relationship between IP and MAC addresses in ver6)

**Neighbor-Advertisement message**
It is a response to a neighbor solicitation message

**Redirection message**
same as in version 4, used to inform the host of the IP address of a better router for data
transmission.
(but now the host can also get the MAC address of the better router)

**Inverse-Neighbor-Solicitation message**
If a node knows the data link address of its neighbor and wants to know the IP
address. The message is encapsulated in an IPv6 datagram which has an all-node
multicast address. The sender must send in the option field:
• Own link-layer address
• Desired neighbor link-layer address
In addition, the sender can insert:
• Own IP address
• MTU (Max Transfer Unit) for the network

**Inverse-Neighbor-Advertisement message**
It is a response to the inverse-neighbor-solicitation message

### Group membership messages
In version 6, the IGMP protocol is eliminated. This functionality is now part of ICMPv6 and
can be accessed with this message type.