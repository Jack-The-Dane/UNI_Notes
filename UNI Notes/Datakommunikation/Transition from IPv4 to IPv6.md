The transition from IPv4 to IPv6 should preferably take place smoothly.
Therefore, the IETF (Internet Engineering Task Force) recommends 3 strategies that can
support this transition:
## Dual Stack
It is recommended that all hosts, before the transition is complete, have a dual
stack of protocols. This means that the host must run IPv4 and IPv6 simultaneously.
To determine which version to use when sending a packet to a destination, the source host
queries the DNS (Domain Name System).
If an IPv4 address is returned, then an IPv4 packet (datagram) is sent and if an IPv6
address is returned, then an IPv6 packet (datagram) is sent.
![[Pasted image 20231031132052.png]]

## Tunneling
When two computers using IPv6 want to communicate, and the packets must
pass a region using IPv4. Then the packets need to have an IPv4 address in this region.
This is done by encapsulating the IPv6 packets in IPv4 packets when they arrive in the IPv4
region and unpacking them to have IPv6 packets when they leave the region. It seems as if
the IPv6 packet enters a tunnel at one end and emerges at the other end.
![[Pasted image 20231031132204.png]]

## Header translation
Header translation is required when the majority of the Internet has moved to IPv6, but some systems still use IPv4. The sender wants to use IPv6, but the receiver does not understand IPv6.
Tunneling does not work in this situation because the packet must be in the IPv4 format to
be understood by the receiver. In this case, the header format must be totally changed
through header translation. The header of the IPv6 packet is converted to an IPv4 header.
![[Pasted image 20231031132250.png]]

