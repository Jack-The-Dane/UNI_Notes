*A datagram can travel through many different networks.*

Every router it encounters:
* decapsulates the IP datagram from the frame it receives
* processes it
* encapsulates it back in another frame.

The format and size of the received frame depends on the protocol used by the physical network where the frame came from.

The format and size of the sent frame depends on the protocol used by the physical network where the frame is going to travel.

**Example:** If a router connects a LAN to a WAN, it receives a frame in the LAN format and sends a frame in the WAN format.

***
A datagram can be fragmented by the source or any router in the path.
* It is fragmented into sizes that meet the requirement of the used data link layer in the network in terms of MTU constraint.

Once a datagram is fragmented, each fragment is independent and will have its own header
* Where most fields are the same.
* But some fields have been changed.

A fragmented datagram may itself be fragmented if it encounters a network with an even smaller MTU. In other words, a datagram may be fragmented several times before it reaches the final destination.
Reassembly of the fragmented datagram is done only at the receiver (not the routers).

***
#### Maximum Transfer Unit (MTU)
![[Pasted image 20231024131718.png]]

***
The IPv4 datagram has 3 fields related to fragmentation and reassembly:
* Identification field.
* Flags field.
* Fragmentation offset field.
![[Pasted image 20231024133055.png]]
The host or router that fragments a datagram must change the values of three fields: flags, fragmentation offset, and total length. The rest of the fields must be copied. Of course, the value of the checksum must be recalculated regardless of fragmentation.

***
#### Identification Field
This 16-bit identification field contains an identification number to identify the source host where the datagram is generated.
* Every datagram sent out from the host has a unique number.
* if a datagram is fragmented, then all fragments get the same identification number copied from the original datagram.

This number helps the receiver to reassemble a datagram. i.e., all fragments with the same number must be assembled into a datagram.

***
#### Flags Field
This field contains 3 bits.
* The first bit is reserved (not used).
* The second bit is called Do not fragment bit.
o If this value is 1, then the datagram must not be fragmented. If the datagram cannot be delivered via some of the available physical networks, it is discarded and an ICMP (Internet Control Message Protocol) error message is sent to the sender.
o If the value is 0, then the datagram can be fragmented if necessary.

* The third bit is called morefragment bit.
o If the value is 1, then it means that the current datagram is not the last one.
o If the value is 0, then it means that the current datagram is the last one (or the only one).
![[Pasted image 20231024133348.png]]

***
#### The fragmentation offset field
This field contain 13 bits and indicates the position of the current fragment relative to the whole datagram. The position is measured in units of 8 bytes.
![[Pasted image 20231024133434.png]]
The value of the offset is measured in units of 8 bytes. This is done because the length of the offset field is only 13 bits long and cannot represent a sequence of bytes greater than 8191, which does not match the datagram's maximum length of 65,535.

Therefore, the offset is specified in units of 8 bytes (8 x 8191 = 65.535 bytes).

This forces hosts or routers that fragment datagrams to choose the size of each fragment so that the first byte number is divisible by 8.

***
#### Example
* The value of the identification field is the same in all fragments (14,567)
* The more bit is set to 1 for all fragments except the last one.
* The value of the offset field for each fragment is shown. if a fragment itself is fragmented, the value of the offset field is always relative to the original datagram (see F2.1 and F2.2).

Note that although the fragments arrived out of order
at the destination, they can be correctly reassembled
by using the following strategy.
1. The first fragment has an offset field value of zero.
2. Divide the length of the first fragment by 8 to get the offset value of the second fragment.
3. Repeat step 2 until a fragment with the more bit value of 0.
![[Pasted image 20231024133618.png]]
