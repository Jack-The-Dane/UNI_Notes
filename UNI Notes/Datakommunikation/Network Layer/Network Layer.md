Routers en route from Alice to Bob are not allowed to
extract the encapsulated data packets unless they
have to be [[Memory Management optimization#Fragmentation|fragmentation]].

If the packet is [[Memory Management optimization#Fragmentation|fragmentation]] at the source or at routers
along the path, the network Layer at the destination is
responsible for waiting until all fragments arrive,
reassembling them, and delivering them to the
upper-layer protocol.

![[Pasted image 20231011211609.png]]