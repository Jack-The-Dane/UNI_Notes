## Basic concepts
CAN – Controller Area Network
▪ In 1982, the development of the CAN bus started at Bosch GmbH®
▪ they wanted a serial bus, which was suitable for use in vehicles
▪ In 1986, this protocol was officially released at the Society of
Automotive Engineers (SAE) conference in Detroit.
▪ The latest specification is CAN 2.0 which came in 1991.
**The specification consists of two parts:**
▪ CAN 2.0A – which uses an 11-bit identifier.
▪ CAN 2.0B – which uses a 29-bit identifier.

The CAN bus is a serial multi-master bus
The CAN bus follows the CSMA (Carrier Sense Multiple Access) design
The new things about CAN are the mechanisms of the access to the
bus. They are:
▪ A distributed nondestructive arbitration mechanism (or Collision
Avoidance (CA))
▪ Error detection and management mechanisms (or fault tolerance)
So, the CAN bus uses CSMA/CA

Both Intel® and Philips®, also including others today, produce controller chips
for CAN using two different solutions.
▪ Intel controllers are often also called FullCAN.
▪ Philips has chosen to do what is called BasicCAN.
FullCAN requires less host CPU power (application programs), since most of
the communication and network management functions are done by the
hardware, i.e., the CAN controller (chip).
BasicCAN has simpler hardware, and to achieve the same functions, more CPU
power (application programs) is required to interface the CAN controller in
order to handle communication and network management.
Other chip manufacturers such as NXP, makes CAN transceiver, to which
you can connect your own microcontroller, and thus get access to the CAN
bus, this solution requires that everything is implemented in software.

But Bosch has also participated in an European collaboration,
through which Bosch made CANopen, an industry standard of
supporting communications inside production cells, which is used in
two areas in particular:
▪ Factory automation
▪ Machine-distributed controls

If you view the protocol from an OSI model perspective:
▪ The CAN protocol stack consists of only the bottom layers
of the OSI model, physical and data link layers.
This design principle has the following benefits:
▪ Implementation is more efficient and inexpensive
▪ Few protocol layers imply less processing delay
▪ Simpler communication software
![[Pasted image 20231208082833.png]]

## Physical and data link layers of CAN
**The Physical layer, this layer takes care of:**
▪ Mechanical and electrical aspects (e.g., voltage levels)
▪ Bit timing
▪ Synchronization
**Medium Access Control (MAC), this sublayer takes care of:**
▪ Arbitration - The bus access mechanism.
▪ Frame encoding and decoding
▪ Error checking and signaling
▪ Fault confinement (e.g., shutdown of faulty devices)
**Logical Link Control (LLC), this sublayer takes care of:**
▪ User interface (API) characterized by a well-defined set of communication services

### Physical layer
![[Pasted image 20231208083020.png]]
The bus terminates with a resistor of 120Ω at each end.
▪ This is used to suppress signal reflections.
▪ Stubs should not be more than 30 cm for the connecting devices if you want to use a speed of 1 MB/s.
![[Pasted image 20231208083235.png]]

#### Transmission media
Two-wire bus:
Pair-twisted double-shielded cable with enhanced immunity to
electromagnetic interferences.
![[Pasted image 20231208083330.png]]
Single-wire bus
▪ This type of bus is simpler and thus also cheaper.
▪ lower immunity to noise and interference.
This type is mostly used in automotive applications.

#### Bit encoding and synchronization
**Bit encoding**
▪ The CAN bus uses an NRZ (non-return to zero) line coding strategy.
**Bit synchronization**
▪ There is no separate clock signal
▪ The edges of the signal itself are used to synchronize the local clock
▪ A Digital-Phase Locked Loop (DPLL) technique is used here to extract the timing information directly from the bit stream.
When the synchronization depends on the edge detection, then we
have to ensure that the data stream contains a sufficient number of
edges. (Too many 0s or 1s can cause sync problems!)

#### Bit stuffing
![[Pasted image 20231208083621.png]]
The rule is as follows:
Five consecutive bits, consisting of either dominant (0) or recessive (1) bits.
Then a complementary bit is inserted at the sender (after CRC calculation)
▪ 11111 → insert a 0
▪ 00000 → insert a 1
The bit is of course removed again at the receiver (before CRC check)
▪ 11111 →remove the next bit
▪ 00000 → remove the next bit

Bit-stuffing may reduce encoding efficiency.
▪ If you look at the theoretical worst case, then the encoding
efficiency can be as low as 80%.
▪ Practical simulations show, however, that only 2-4 bits are
inserted in each frame.
▪ Bit-stuffing is not applied to all fields in a frame. Only applied
to fields from the SOF bit up to the CRC sequence.
![[Pasted image 20231208083743.png]]

### Data link layer
#### MAC Layer: Frame format
CAN specification defines both a standard (CAN2.0A) and an extended (CAN2.0B) frame format.
![[Pasted image 20231208083930.png]]

#### Frame types:
There are 4 different frame types:
▪ Data frame
▪ Remote frame
▪ Error frame
▪ Overload frame

##### Data frame CAN2.0A
![[Pasted image 20231208084121.png]]
**SOF**
A Data frame starts with a Start of Frame bit (SOF).
▪ SOF is a dominant bit (logic 0) 0 is dominant because only one device needs to pull the bus to zero, to make all other nodes read zero.
▪ SOF indicates the start of a frame just as in a conventional UART
▪ SOF is also used to synchronize the receiving nodes
This field is part of the bus access mechanism (arbitration) but is
also part of the protocol frame check mechanism
**Identifier field**
The identifier field identify uniquely the content of the frame
▪ The number in this field is unique across the entire network
▪ The MAC uses the field number for access control on the bus
▪ Lower number has higher priority, when multiple nodes are trying to talk simultaneously
▪ The Wired-AND technique determines who gets access to the bus.
This field is part of the bus access mechanism (arbitration)
**Remote transmission request (RTR)**
▪ The field distinguishes between data and remote frames
▪ If the value is dominant (logic 0), then it is a data frame
▪ If the value is recessive (logic 1), then it is a remote frame
▪ According to the Wired-AND technique, data frames have
higher priority than remote frames
This field is part of the bus access mechanism (arbitration).
**Identifier extention (IDE)**
▪ This field indicates whether it is a CAN 2.0A or CAN 2.0B frame
▪ If the value of the field is dominant (logic 0), it is a CAN 2.0A
frame
**Reserved bit (r0)**
▪ The value of the field is dominant (logic 0)
This field is part of the protocol frame check mechanism
**Data length code (DLC)**
▪ The field is 4 bits long
▪ The value of the field indicates the length of the data field in bytes
▪ The value of the field must be between 0 and 8
▪ Values between 9 and 15 can be used in specific applications
▪ If values between 9 and 15 are used, then the length of the data
field is supposed to be 8 bytes
**Data field**
▪ The field contains the actual payload
▪ The short length of the field ensures a quick response, as
the bus becomes available quickly.
▪ The short length of the field minimizes priority inversion
phenomenon.
**Data field**
▪ The field contains the actual payload
▪ The short length of the field ensures a quick response, as the bus becomes available quickly.
▪ The short length of the field minimizes priority inversion phenomenon.
**CRC field**
▪ The field is a total of 16 bits long (15 + 1)
▪ The CRC used is a CRC15 (x15 + x14 + x10 + x8 + x7 +x4 +x3 + x0)
▪ CRC is performed on all bits between SOF and CRC
▪ The last bit is a delimiter and recessive (logic 1), which is used
to separate this field from the next field, at the same time, the
bit is part of the protocol frame check mechanism
▪ CRC is performed before bit-stuffing
**ACK field**
▪ This field is a 2 bit long, the first bit is the ACK field itself
▪ The sender set this bit as recessive (logic 1)
▪ All nodes that receive the frame correctly overwrite the bit as dominant
(logical 0).
▪ If the sender reads this bit as dominant, then the sender knows that
the frame is received successfully by at least one node.
▪ Last bit is a delimiter and resistive (logic 1), which is used to separate it from
the next field, at the same time, the bit is part of the protocol frame check
mechanism.
**EOF field**
▪ The field is 7 bits long
▪ All bits are recessive (logic 1)
▪ The field indicates the end of a frame
This field is part of the protocol frame check mechanism
**Intermission (IMS) field**
▪ The field is 3 bits long
▪ All bits are recessive (logic 1)
▪ The field separates consecutive frames exchanged on the bus

##### Data frame CAN2.0B
![[Pasted image 20231208085219.png]]
**Substitute remote request (SRR)**
▪ This field is a placeholder that is used to preserve the structure of the frames
▪ The value in this field is recessive (logic 1)
**The identifier extension field identify uniquely the content of the frame**
▪ The number in this field is (together with the base ID) unique on
the whole network.
▪ The MAC uses the field number (together with the base ID) for
access control on the bus.
▪ Lower number has higher priority.
▪ The Wired-AND technique determines who gets access to the bus
This field is part of the bus access mechanism (arbitration)
**Reserved bits (r0, r1)**
▪ The values of the fields are dominant (logic 0)
The field is part of the protocol frame check mechanism

##### Remote frame
Remote frames are similar to data frames except that remote frames do not carry any data and do not have a data field.
Remote frames are used to request that a given data frame is sent from another node (remote node) on the network.
It is up to the receivers to discover the one that has to reply.
![[Pasted image 20231208085415.png]]
▪ In a remote frame, RTR is set to recessive (logic 1).
▪ DLC indicates the length of data that the sender of a remote frame wants to receive.
Note this is NOT the length of the data field in the sender
remote frame, but the length of what is to be sent back from a
remote node.
Remember that a data frame with the same identifier as a remote
frame sent at the same time will win the bus access because of the
way the RTR bit is encoded.

##### Error frame
This type of frame is used to notify the nodes in the network
that an error has occurred.

**If the node that detects the error is in Error-Active mode, then
the Error frame will look like this:**
![[Pasted image 20231208085606.png]]
▪ First, 6 dominant bits are sent (logic 0)
▪ This action violates the bit-stuffing rule!
▪ All other nodes see this violation
▪ And sends Echo Error flags, which are 6 dominant bits (logical 0)
▪ Finally ends with 8 recessive bits (logic 1)
▪ The sending node, which was interrupted, retransmits its frame

**If the node that detects the error is in Error-Passive mode, then
the Error frame will look like this:**
![[Pasted image 20231208085745.png]]
▪ First, 6 recessive bits are sent (logic 1)
▪ Finally ends with 8 recessive bits (logic 1)
▪ This action will NOT disturb the traffic on the bus remember wired-AND
So, unless the sending node or an error-active node discover the
error, then nothing happens

###### Error-active/passive mode
The rules for active and passive error modes are used in a fault confinement mechanism of CAN specification.
A node can be in the following three states:
▪ Error-active Here the traffic is interrupted by an active error frame
▪ Error-passive As we have just seen, this does NOT disturb the traffic on the bus
▪ Bus-off Here the node interrupts itself and does not transmit anything
There are two counters:
▪ Transmission error count (TEC)
▪ Receive error count (REC)
A faulty transmission will increment the counter up by more than 1
A correct transmission will decrement the counter down by 1
When any counter value 127 is exceeded: Error-active → Error-passive
When any counter value 255 is exceeded: Error-passive → Bus-off

###### Error Detection Mechanisms
▪ Cyclic redundant check (CRC): Each message features a 15-bit Cyclic Redundancy Checksum, and any node that detects a different CRC in the message than what it has calculated itself will signal an CRC Error.
▪ Frame check: fixed fields (delimiters and EOF) are examined for their expected values.
▪ ACK check: the sender examines whether the ACK flag is dominant, if not, then an error has occurred.
▪ Bit monitoring: The sending node checks the sent signal level on the bus in relation to what it sent.
▪ Bit stuffing: each node checks if this rule is complied with, sends an error frame, if not.
All these mechanisms ensure that the probability of an error not
being detected is: 4.7·10-11

##### Overload frame
▪ This frame type is used by slow nodes to slow down (extend the time in between data frames).
A maximum of two overload frames may delay the start of the next message.
▪ Or by any node else that detects a dominant bit (logic 0) in the Intermission (IMS) field.
There should be three recessive bits in the IMS field
![[Pasted image 20231208091017.png]]
Unlike an error frame, which interrupts a transmission, an overload frame is sent only in between frames in the IMS phase.
The speed of CAN controllers today makes that frame type useless

#### Arbitration - The bus access mechanism
![[Pasted image 20231208091308.png]]
▪ Because of the wired-AND property of the bus, collisions are avoided thanks to the binary countdown technique.
▪ Nodes that lose arbitration try to resend the frames when possible (after the current transmission).

## Producer / Consumer model for information exchanges
![[Pasted image 20231208091513.png]]
Because of the broadcast nature of the CAN bus, it is possible for several nodes to subscribe to the same messages
▪ It is not the nodes that have addresses/identifiers (node addressing)
▪ It is the messages that have unique identifiers/addresses (object addressing)

## Single wire CAN Network
![[Pasted image 20231208091642.png]]
![[Pasted image 20231208091703.png]]![[Pasted image 20231208091723.png]]
