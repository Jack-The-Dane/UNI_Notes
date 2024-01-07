If this method is used, then there is a relationship between all packets belonging to the same message. Before all packets in a message can be sent, a virtual connection should be set up to define the path for the datagrams. After connection setup, the datagrams can all follow the same path. A flow label, a virtual circuit identifier, is used to define the path.
![[Pasted image 20231011214257.png]]

The datagram is packaged with the flow label. And the router uses this info for forwarding.
![[Pasted image 20231011214407.png]]

#### Setup Phase
Field, Outgoing Label, is reserved in all routers' forwarding tables with Request packet.
![[Pasted image 20231011214457.png]]
The setup phase
1. A sends a request packet to R1
2. R1 receives the package. It can see that the connection must go from A to B through its own port 3. R1 creates a line in its forwarding table, but can only fill in 3 of the 4 fields:
* Incoming port = 1
* Incoming label = 14 (R1 chooses it by itself)
* Outgoing port = 3 (a ”knowledge” that R1 has based on destination B)
* Outgoing label = ? (just as R1 itself has chosen its label 14, so R3 will do so too, but R1 does not know it yet)
3. A request packet is sent from R1 to R3 which also reserves a line in its table,
fills it in and sends a request packet on to R4 etc. …
4. B receives the Request packet from R4, if it is ready to receive data from A,
then it sends an Ack packet (here with a label = 77) back to R4

![[Pasted image 20231011214818.png]]
R4 can now fill in its missing field in its forward table and send an Ack packet to R3 which can then fill in its missing field etc…
