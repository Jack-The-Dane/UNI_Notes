* When we use classless addressing, it is likely that the routing tables will be larger in size.
* This is because the whole idea of classless addressing is to divide the entire address space into smaller address blocks that are easier to handle.
* As the tables get larger, so does the search time in them.
* To address this issue, the idea of address aggregation was designed.

***
#### Example
![[Pasted image 20231024123025.png]]
* Router R1 is connected to 4 organizations (companies), each using 64 addresses.
* Router R2 is somewhere far from router R1.
* Router R1 has a long routing table (here 4), as each packet must be routed correctly to each organization.
* But router R2, in turn, has a small routing table.
* Here, all packets with addresses from 140.24.70.0 to 140.24.70.255 are sent via I/O m0 regardless of which organization they belong to. This is called address aggregation.

>Note, however, that router R2 would have a larger routing table if the 4 address blocks can not be aggregated into a larger block.

***
#### Address Aggregation - Longest mask match
*What if e.g., organization 4 geographically is far from the others, can we still apply address aggregation?*

The answer is yes! Notice that the routing tables are arranged so that the entries in the forwarding table are sorted from the longest mask to the shortest mask.
This is called: Longest mask match.
![[Pasted image 20231024123310.png]]
Assume that a packet arrives at R2 with organization 4 as the destination address 140.24.7.200.
1. First mask (/26) bit-wise AND with the destination address. The result gives 140.24.7.192, which matches the network address in row 1. The next-hop address (the destination address in this case) and the router interface number (m1) are passed on to ARP for further processing.
The packet reaches organization 4 as it should.

>Note here that if mask /24 had been first in the table at R2, then the packet would have mistakenly ended up at router R1!