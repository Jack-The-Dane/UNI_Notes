To solve the problem of gigantic forwarding tables, we can create a kind of hierarchy in the forwarding tables.
So how does this reduce the size of the routing tables?
* The rest of the Internet does not need to know about this division that the ISP has made inside a network.
* All packets intended for an address in this large block are sent to the ISP.
* This only provides one entry in all routers in the world for all the customers who belong to this ISP.

Of course, routers inside this local ISP must know sub-blocks and are able to forward
the packets to specific customers.

***
#### Example
![[Pasted image 20231024123600.png]]
**A regional ISP** gets 16.384 addresses with the starting address 120.14.64.0 The regional ISP divides these addresses into 4 sub-blocks, each with 4.096 addresses.
These sub-blocks are now assigned to 3 local ISPs (sub-block 2 is saved for future use) 
>Note that the mask for each sub-block here is /20. The original block had the mask /18 

**The first local ISP** has divided its addresses into 8 smaller blocks, each of which is assigned a small ISP.
Each of these small ISPs further divides their address block into 128 households (H001-H128) Each of these households has 4 addresses. (232-30 = 4 pcs.) 
>Note that: small ISP has the mask /23 and every household has mask/30

**The second local ISP** has divided its block into 4 smaller blocks. Each of these blocks is assigned to large customers (LOrg01 –LOrg04) with 1024 addresses and a mask of /22. 

**The third local ISP** has divided its block into 16 smaller blocks.
Each of these blocks is assigned to small customers (SOrg01 – SOrg16) with 256 addresses and a mask of /24.


There is a kind of hierarchy in this setup:
All routers on the Internet send packets with addresses from:
120.14.64.0 – 120.14.127.255 to the regional ISP.

The regional ISP sends packets with addresses from:
120.14.64.0 – 120.14.79.255 to the first local ISP.

The first local ISP sends packets with addresses from:
120.14.64.0 – 120.14.64.3 to household H001.
