We have previously talked about error detection and error correction.
Although error control can also be implemented here at the network layer, We choose not to do it in the Internet. One of the reasons is that packages can be fragmented, which makes error checking at this layer very inefficient.
However, a checksum field has been added to the datagram so that you can check if the header is corrupted or not.
Note that this only applies to the header, not the entire datagram!
It should also be mentioned here that although the network layer does not directly provide error control functionality, an auxiliary protocol is used ”Internet Control Message Protocol (ICMP)”,
which is used when datagrams are discarded or have unknown information in the header.
