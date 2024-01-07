**Congestion control** is a topic that the network layer needs to address.

Network congestion occurs when there is too much data traffic (too many datagrams) in an area of the Internet.
If a computer has more capacity than the network and the routers it is connected to, then congestion can occur.
In such situations, some routers may drop some of the datagrams, but due to the error control handled in the upper layers, the lost datagrams are re-transmitted. This can lead to further congestion and perhaps eventually collapse.
Congestion control in the network layer will be discussed (even if it is not implemented in the Internet)