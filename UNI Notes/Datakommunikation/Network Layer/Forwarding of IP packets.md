#### Forwarding of IP packets (based on destination address)
![[Pasted image 20231024122804.png]]
* Destination address and the mask (/n) are used.
* This result is compared with the network addresses (in column 1).
* When a match is found, the Next-hop address (column 2) is used to (via ARP) find the link layer address to be used in the frame to be forwarded.
* Column 3 indicates which output interface of the router the frame is to be sent from.

***
#### Example
![[Pasted image 20231024122852.png]]

***
#### Forwarding of IP packets (based on labels)
In the 1980s, an effort started to somehow change IP to behave like a connection-oriented protocol in which the routing is replaced by switching.

In a connectionless network (datagram approach), a router forwards a packet based on the destination address in the header of the packet. On the other hand, in a connection-oriented network (virtual-circuit approach), a switch forwards a packet based on the label attached to
the packet

* Connectionless: datagrams are forwarded based on their destination address by routers.
* Connection-oriented: datagrams are forwarded based on labels attached to them by switches.

>Note that: routing is normally based on searching the contents of a table; switching can be done by accessing a table using an index. In other words, routing involves searching; switching involves accessing.

***
##### Forwarding of IP packets – Routing Example
![[Pasted image 20231024124443.png]]

***
##### Forwarding of IP packets – Switching Example
![[Pasted image 20231024124507.png]]
