* One problem of the distribution of addresses through ISPs is that the ISP may not be able to grant the increasing demand when a business grows and needs more addresses because the addresses before and after the range may have been already allocated to other networks.
* However, only few addresses are needed for universal communication while many private block addresses can be used for internal communication.
* A technology that can provide the mapping between the private and universal addresses is Network Address Translation (NAT).
![[Pasted image 20231024122042.png]]

***
NAT can only be done via a NAT-capable router that runs NAT software.
![[Pasted image 20231024122200.png]]
* In all outgoing packets, the source address is replaced with the global address of the NAT router.
* In all incoming packets, the destination address is changed from the NAT router's global address to appropriate private address.

***
![[Pasted image 20231024122223.png]]
Replacing the source address in the outgoing packets is straightforward.
But how can the NAT router know the destination address of a packet coming from the Internet?
* This problem is solved with a translation table, internally in the NAT router.

![[Pasted image 20231024122316.png]]
>The use of only one global address by the NAT router allows only one private-network host to access a given external host.

***
**A pool of IP addresses:** Since a NAT router only has one global address, only one host
from the private network can access an external host.

To remove this restriction, the NAT router can use a pool of global addresses e.g., 4
global addresses: 200.24.5.8; 200.24.5.9; 200.24.5.10; 200.24.5.11

Now up to 4 hosts from the private network can communicate with the same external
host.

**Drawback:** No private-network host can access two external server programs on the
same host (e.g., http and FTP).


***
**Both IP address and port number:** in order to allow a many-to-many mapping relationship between hosts of a private network and external server programs, more information can be provided in the translation table.
Example: two hosts with the addresses 172.18.3.1 and 172.18.3.2 (from the private network) want to access a HTTP server on an external host with the address 25.8.3.2.
![[Pasted image 20231024122542.png]]
>Note that when a response from HTTP comes back, it is the combination of the source address 25.8.3.2 and the destination port number 1400 or 1401 that defines the host on the private network. 
>
>Also note that to make this work, the private port numbers must be unique.
