## Framing
The bit stream of the data link layer is packed into structures called frames, so that each frame can be interpreted individually.
Frames can be of both fixed (Wide area networks) and variable sizes (most LAN networks).
For variable-sized framing two methods are used; character oriented and bit-oriented.

### Character-oriented framing (byte-oriented)
![[Pasted image 20230926122841.png]]The flag is used to indicate the end of a frame, and should be a character that will never naturally occur in the data stream. This can be mitigated by using escape codes or byte stuffing:
![[Pasted image 20230926123123.png]]
The character-oriented protocols have a problem, that most universal coding systems use 16 or 32-bit encoding, which clashes with the 8-bit nature of characters.

### Bit-oriented framing
![[Pasted image 20230926123309.png]]
![[Pasted image 20230926123351.png]]

## Flow and error control
![[Pasted image 20230926123450.png]]
The primary method of error control in the data link layer is retransmission. This method is called Automatic Repeat reQuest (ARQ).

### Finite State Machine
![[Pasted image 20230926123925.png]]

### Simple protocol
![[Pasted image 20230926123954.png]]
![[Pasted image 20230926124058.png]]

### Stop-and-Wait protocol
![[Pasted image 20230926124130.png]]
![[Pasted image 20230926124229.png]]
![[Pasted image 20230926124338.png]]
![[Pasted image 20230926124353.png]]
The number of the ACK frame, is the frame number that the receiver expects to receive next.
#### Sequence numbering
![[Pasted image 20230926125246.png]]
The number of bits need for sequence numbering depends on how many frames can be in the channel at one time. 

### Piggybacking
![[Pasted image 20230926125458.png]]
This enables the sender and receiver to send an ACK frame while also sending a new frame of data. Effectively doubling effeiciency, by making communcation two-way.
