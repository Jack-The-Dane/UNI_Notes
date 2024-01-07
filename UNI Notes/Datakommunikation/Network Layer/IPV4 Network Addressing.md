
The first address in the network (block) is called network address, which is particularly important because it is used in routing a packet to its destination network.
Let us assume that the Internet consists of *m* networks and a router with *m* interfaces (ports).
When a packet arrives at the router from any source host, the router needs to know which network the packet should be sent to: from which interface the packet should be sent out.
![[Pasted image 20231012103633.png]]
Once the network address is found, the forwarding table is consulted to find the interface number, from which the packet should be sent out.

#### Subnetting
More levels of hierarchy can be created using subnetting. An organization (or an ISP) that has been assigned a large block may want to divide the block into different subnetworks or subnets.
* The outside world still view the organization as a single network, but internally there are several different subnets.
* All data is sent to a router connected to the rest of the Internet.
* The router also forward data to the relevant subnets.

>The network block has one mask, and each subnet inside also has their own mask.

***
##### Subnetting Design
It is important that subnets are designed with care so that it is possible for a router to route packets to the relevant subnets.
Designing subnets If an organization has been assigned *N* addresses (the prefix length is n) the block is divided into subnets, the assigned number of addresses in each subnetwork is $N_{sub}$. Then the following procedure should be followed:
* The number of addresses in each subnet must follow n-th power of 2 (1, 2, 4, …)
* The prefix length in each subnet is found as $n_{sub}=32-\log_{2}(N_{sub})$.
* The starting address of a subnet must be divisible by the number of addresses in the subnet

##### Subnetting Example
![[Pasted image 20231012104219.png]]

![[Pasted image 20231012104233.png]]
![[Pasted image 20231012104245.png]]
![[Pasted image 20231012104254.png]]
![[Pasted image 20231012104300.png]]
![[Pasted image 20231012104310.png]]
![[Pasted image 20231012104320.png]]
![[Pasted image 20231012104325.png]]
![[Pasted image 20231012104336.png]]

***
#### Address Aggregation
One of the advantages of the [[IPV4 Addressing#CIDR Example|CIDR]]  strategy is address aggregation. When blocks of addresses are combined to create a larger block, routing can be done based on the prefix of the larger block.
All packets for the large block is sent to a router connected to the smaller blocks.
This router (here ISP) then forward the packets to the right subnets.
![[Pasted image 20231012104448.png]]

***
#### Special Addresses
Before we end the topic of addresses in IPv4, we just need to mention some special addresses:

* This-host address
* Limited broadcast address
* Loop-back address
* Private address (NAT)
* Multicast address

This-host address: 0.0.0.0/32 this address is used when a host needs to send an IP datagram but does not know its own IP address to use as the source address.

Limited-broadcast adressen: 255.255.255.255/32 this address is used when a router or host needs to send a datagram to all devices in a network.
Note that such a datagram can NOT leave the network!
Routers in the network block further transmission out of the network (hence the word Limited)
![[Pasted image 20231012104654.png]]
