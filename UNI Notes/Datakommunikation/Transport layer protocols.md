## Simple protocol
This protocol has neither Flow nor Error control, where the packets move in one direction.
• assume the receiver can handle all packets it receive immediately.
• and it immediately removes packet header and passes data on to the application layer without any delay.
• In other words, we imagine that the receiver will never be overwhelmed with too
much incoming data.
![[Pasted image 20231107122149.png]]
There is no need for flow control as the processing of packets on both the sending and receiving side is immediate.
![[Pasted image 20231107122339.png]]

## Stop-and-Wait protocol
Here, a simple error control mechanism is added to the protocol, which makes it possible to find and correct errors.
In order to find and correct errors in the sent packets, we need to add redundant bits to our packets. (Checksum or CRC)
When a package is received, it is examined for errors 
	• If it is defective, it is simply discarded
When an error is found, cf. this protocol, this is manifested by a receiver
remaining silent. (an acknowledgement will be sent back if no error)

Packets lost during transmission are more difficult to handle
The received packet could be:
	• Correct
	• Duplicate
	• Out of order (and we could not know the order)
The solution is to number the packets with sequence numbers,
then the recipient can determine if the received packet is in the right order or if
it is out of order.
	• If so, then other packets are either lost or duplicated.

Corrupted or lost packages must be retransmitted, cf. this protocol.
	• If the receiver does not respond, then an error has occurred.
	• The sender who saves a copy of the sent packet starts a timer at the time of dispatch.
If no ACK is received before the timer expires, the packet is retransmitted and the timer is restarted.
The copy is saved until an ACK is received before the timer expires.
Since an ACK packet can also be damaged and lost, they must also have redundant bits and a sequence number.
In this protocol, corrupted ACK packets are discarded and out-of-order ACK packets are ignored.
![[Pasted image 20231107122811.png]]
**Sequence numbering**
An important consideration here is how many different sequence numbers we need to
have in order to make a unique communication.
Sequence numbers can wrap around.
• This means that if you have a sequence number field of m bits, then sequence
numbers can go from 0 to 2m‐1, then they are repeated.
In this protocol only 2 different sequence numbers (1 bit) are needed since receipt
(ACK) for each packet is arrived before the next is sent.
An ACK packet, sent as a receipt for a correctly received packet, contains
the sequence number of the next packet that the receiver expects to
receive.
### Example
![[Pasted image 20231107123137.png]]

## Go-Back-N protocol
The problem with the previous protocol is that we only send one packet when we have received a receipt (ACK) that shows the previous packet has been received correctly.
Therefore, we are now expanding this protocol so that we can send more than one packets while the sender is waiting for acknowledgement. In other words, multiple packets must be in transition to keep the channel busy.
![[Pasted image 20231107123426.png]]
**Sequence numbering**
Also, in this protocol we have a field in the header for numbering the packets, and here it
also applies that we use modulus $2^m$. Thus, the numbering for m bit, goes from 0 to $2^m‐1$.
**Sliding Window**
Once we have determined a number of sequence numbers we will apply, then it is
important to understand that we can only use less than $2^m$ numbers in a sender sliding
window, which means that the sender can only have a limited number of outstanding
packets, i.e., sent packets that have not yet been acknowledged

### Sender window
![[Pasted image 20231107123736.png]]
• The packets acknowledged (far left), the sender no longer has copies of them.
• The packets in the dark field, the sender needs to have copies of them, as their fate is not known yet, we do not know if they should be resent later yet.
• To the right of the dark block, the range of sequence numbers for packets that can be sent. However, the corresponding data have not yet been received from the application layer.
### Receiver window
The receiver's window is of only size 1.
The receiver only waits for a specific packet (here 5), all other received packets are
discarded and must be retransmitted.
![[Pasted image 20231107123952.png]]

### Timers
Only one timer is used here.
The timer is set all the time so that it reflects the time of dispatch of the oldest packet (the first outstanding packet) that has not yet been acknowledged.
If the timer expires, all outstanding packets are retransmitted. That is why the protocol is called Go-Back-N. On a time-out, the machine goes back N locations and resends all packets.

### Sender windows size
Now we need to see why the window should be less than 2m.
**Example**
We choose m=2.
The size of the window is selected: 2m‐1 = 3.
In the figure , a window size of 3 (a) is compared against with one of 4 (b).
• If the window is 3 (i.e., less than $2^2$) and all receipts are lost, then the timer for packet 0 will expire and all three packets will be retransmitted. Nothing special would happen.
• If the window is 4 (i.e., equal to 22) and all receipts are lost, then the timer for packet 0 will
expire and all four packets will be retransmitted.
But at that point, the receiver expects packet 0 and mistakenly accepts the resent packet 0 as a new packet 0.
![[Pasted image 20231107124332.png]]
Accumulative acknowledgements can also improve effeciency of this protocol. That is an acknowledgement of one packet will also be an acknowledgement of all previous packets.
Drawback of this protocol is that when one packet is not acknowledged and the timer expires, all of the packets since the unacknowledged packet have to be retransmitted.
## Selective-Repeat protocol
The Go‐Back‐N protocol simplifies the process on the receiver side.
Here you only need to keep track of one variable, and you do not need any buffers to keep track of out-of-order packets, they are simply discarded.
All these nice things have their "price": This type of protocol is very inefficient when the network layer loses many packets.
The Selective Repeat protocol resend only selective packets that are actually lost, not all the outstanding packets.
This is more efficient, but it also means that the receiver becomes more complex.

On the sender side, the window is similar to the one from the Go‐Back‐N, it's just smaller. Later we will see why the size is smaller.

The receiver window in Selective-Repeat is totally different from the one in Go-Back-N. The size of the receiver window is the same as the size of the sender window.
![[Pasted image 20231107125210.png]]
### Sender window
![[Pasted image 20231107125247.png]]
On the sender side, the window has become a little more complex
• The red boxes are packets for which the receipts (ACK) have not yet been received.
• The gray box is a packet for which the receipt (ACK) has been received (but out of order).
When packets 0 and 1 are acknowledged, the window will slide by three boxes to the right.

### Receiver window
![[Pasted image 20231107125333.png]]
On the receiver side, the window has become more complex.
• The gray boxes are packets received out-of-order.
• The white boxes are the expected packets.
In this case, the window will slide by two boxes to the right when the packet 3 is received, because then packets 3 and 4 will be in order, and they can thus be delivered on up to the application layer.

### Window size
We will now show why the size of the window may only be up to half of $2^m$ (m is the number of bits in the sequence numbering)
E.g., m = 2 (numbers from 0 to 3), which means that the maximum window size is $2^m/2 = 2$.
The figure in the next slide compares a window of size 2 and another one of size 3.
• If the window size is 2 and all ACKs are lost, then timer 0 will expire and packet 0 will be resent.
But the receiver is waiting for packet 2, not packet 0, so this duplicate is discarded. Which is correct.
• If the window size is 3 and all ACKs are lost, then timer 0 will expire and packet 0 will be resent. The receiver is waiting for a new packet 0 rather than the old packet 0 which is resent. The receiver mistakenly accepts this duplicate. Which is wrong.
![[Pasted image 20231107125932.png]]

## Bidirectional protocol
All the protocols we have viewed here are unidirectional protocols.
But in the real world, bidirectional communication is usually used.
• Therefore, receipts (ACK) to be returned to a sender are embedded in the packets sent the other way around, and vice versa.
• Thus, a packet header will contain both a sequence number for what is sent and an ACK number for what is received.
### Piggybacking
![[Pasted image 20231107130841.png]]
### Reliability
One of the questions you might ask yourself is:
If the Data Link layer is reliable and offers flow and error control (as we have seen that before), then do we also need to have flow and error control on the Transport layer?
The answer is YES !
Reliability on the Data Link layer is between two nodes!
We also need reliability between two ends (process to process)!


