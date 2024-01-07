During the 1980s, several manufacturers developed routers that implement switch technology. Later, IETF (Internet Engineering Task Force) approved a standard, called Multi-Protocol Label Switching ( MPLS).

These routers can then replace conventional routers.
* These routers can forward packets based on the destination address,
* But also behave like a switch when packets need to be forwarded based on labels.

**A new header**
To be able to simulate connection-oriented switching using protocols such as IP, you need to add an extra field to the packet that contains the label.

>[[IPV4]]does not allow this extension. (but IPv6 does!)


***
#### The Solution
Encapsulate the IPv4 datagram in an MPLS packet.
Here MPLS will simulate a layer between the [[Data Link Layer]] Layer and the [[Network Layer]].

The whole IP packet is encapsulated as the payload in an MPLS packet and an MPLS header is added.
![[Pasted image 20231024125159.png]]

In fact, the MPLS header is a stack of sub-headers used for multilevel hierarchical switching.

**Label field:** This 20-bit long field defines the label used to index the forwarding table in the router.

**Exp field:** This 3-bit field is reserved for experimental purposes.

**S field:** This field of only 1-bit indicates the end (S = 1) of the stack of sub-headers.

**TTL field:** This 8-bit long field is similar to the TTL (Time To Live) field in an IP datagram.
Each visited router decrements the value in this field by one. When it becomes 0, the packet is discarded to avoid looping.

***
A Stack of labels in MPLS, allows hierarchical switching.
> This is similar to conventional hierarchical routing (as we have seen before)

E.g., a packet with two labels can use the top label to forward the packet through switches outside an organization; the bottom label can be used to forward the packet inside the organization to reach the destination subnet.