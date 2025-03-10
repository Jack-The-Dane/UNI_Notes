#datalink #layer
![[Pasted image 20230919123000.png]]

Services:
#services
![[Pasted image 20230919122321.png]]

The data link layer can control how a medium is used, it can either use the full capacity of the link, if operating point-to-point, or it can use only part of the link, if broadcasting to many points.
Two sublayers:
![[Pasted image 20230919123237.png]]

Three types of addressing:
#addressing
![[Pasted image 20230919123603.png]]

ARP
![[Pasted image 20230919124000.png]]
![[Pasted image 20230919124029.png]]
![[Pasted image 20230919124043.png]]

## Error detection and types
### Error types
#error #types

Single bit error:
![[Pasted image 20230919130136.png]]

Burst error:
![[Pasted image 20230919130155.png]]

### Error detection and correction
#error #detection
- Redundancy is the central concept in error detection and correction
	- The redundant bits are added by sender and removed by receiver
	- Their presence allows the receiver to detect and possibly correct corrupted bits.

### Block coding
#block
One method to do error detection, using datawords and codewords
![[Pasted image 20230919130614.png]]
This method is limited by the fact that a valid codeword can be corrupted in to a different valid codeword, then the error cant be detected.

### Hamming distance
#hamming
Hamming distance between two datawords of the same size is the number of different bits when the datawords are compared bit by bit.
![[Pasted image 20230919131852.png]]
The minimum hamming distance signifies how many bits have to be flipped for a valid codeword to be corrupted in to a different valid codeword. The higher, the better.
![[Pasted image 20230919132226.png]]

### Linear block coding
#linear #block #coding
Linear block coding is a code in which the XOR operation of two valid codewords will create another valid codeword. The minimum hamming distance for a linear block code is the number of 1s in the nonzero valid codeword with the smallest number of 1s.

### Parity-Check code
#parity #paritycheck
![[Pasted image 20230919132918.png]]

### Cyclic codes
#cyclic
Cyclic codes are special linear block codes with one extra property. in a cyclic code, if a codeword is cyclically shifted (rotated), the result is another codeword.

Cyclic redundant check:
![[Pasted image 20230919133305.png]]
![[Pasted image 20230919133345.png]]

Polynomials:
![[Pasted image 20230919134032.png]]

Cyclic code analysis:
# All division signs after this text are modulo operations

![[Pasted image 20230919134152.png]]
![[Pasted image 20230919134209.png]]

Single bit error detection:
![[Pasted image 20230919134923.png]]

Two isolated single bit errors:
![[Pasted image 20230919135106.png]]

Odd number of errors:
![[Pasted image 20230919135505.png]]

Burst error:
![[Pasted image 20230919135844.png]]
![[Pasted image 20230919135914.png]]
![[Pasted image 20230919135932.png]]

Generator Polynomials:
#generator #polynomials
![[Pasted image 20230919140443.png]]
