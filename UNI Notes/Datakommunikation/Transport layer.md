Transport Layer is located between the Application Layer and the Network Layer.
It provides process-to-process communication between two Application Layers, one on each host. The communication takes place via a logical connection between the two hosts, each of which can be in different sites of the globe.
![[Pasted image 20231031132615.png]]

## Service
The transport layer ensures that data is delivered SAFELY from one process
(running program) on one computer (host) to another process (running program)
on another computer (host).(by safe flow and error control)
**The Data Link layer** is responsible for node-to-node communication (Frames are sent
between neighboring nodes on a LAN)
**The Network layer** is responsible for host‐to‐host communication (Datagrams are sent
between hosts on the Internet.)
**The Transport layer** is responsible for process‐to‐process communication.
![[Pasted image 20231031132737.png]]

## Addressing
We need to have an addressing system so that we can distinguish different processes on
a host. The address in this transport layer is called a port number.
This address has 16 bits, giving 65,536 different addresses (0 - 65,535)
The client program defines itself by a port number (ephemeral port number). This (random)
number is selected by the transport layer software running on the client's host.
The server process must also define itself by a port number. This port number, however,
cannot be chosen randomly (otherwise the client could not find the server).
It has been decided by TCP/IP to use universal numbers for servers, that is, well-known
port numbers.

### Example
![[Pasted image 20231031132937.png]]
It should be clear that the IP address and port number have their different roles to play when finding the final receiver of some data.
IP address selects the host among the different hosts in the world.
Port number selects a specific process on this selected host.
![[Pasted image 20231031133027.png]]

## ICANN Range
Internet Corporation for Assigned Names and Numbers (ICANN) has divided port
addresses into 3 ranges:
• Well-known ports: these are numbers in the range 0 – 1,023 and are assigned and
controlled by ICANN.

• Registered ports: these are numbers in the range 1,024 – 49,151 and are not
assigned or controlled by ICANN. They can be only registered with ICANN to
avoid duplication.

• Dynamic ports: these are numbers in the range 49,152 - 65,535 and are neither
registered nor controlled. They can be assigned to any process, and these are the
temporary ports.

## Socket Addresses
Process-to-process communication requires two identifiers:
• IP address
• Port number
The combination of an IP address and a port number is called a Socket address.
• The client socket address uniquely identifies the client process!
• The server socket address uniquely identifies the server process!
![[Pasted image 20231031133257.png]]

## Encapsulation and decapsulation
In order to be able to send a message from one process to another, the transport layer protocol has to encapsulate and decapsulate the messages.
![[Pasted image 20231031133344.png]]
• Encapsulation happens at the sender site. When a process wants to send a message, it is delivered to the transport layer with a pair of socket addresses (sender/receiver) and some other information depending on the transport layer's protocol.
• Decapsulation happens at the receiver site. When the packet arrives at the receiver.
The header of the packet is removed, and data is delivered to the process specified by the port address. The sender socket address is also handed over to the process in case it needs to respond to the received message.

## Multiplexing
On the sender side, there can be many processes that need to send packets. However,
only one transport layer protocol is available. This is called a many‐to‐one relationship
and requires multiplexing.

## Demultiplexing
On the receiver side, the transport layer protocol accepts messages from different source
processes and distributes them to the correct destination processes according to their
port numbers. This is a one-to-many relationship and requires demultiplexing.

## Flow control
Whenever an entity produces items and another entity consumes them, there should be a balance between production and consumption rates.
If the items are produced faster than they can be consumed, the consumer can be overwhelmed and may need to discard some items.
Flow control is needed to prevent losing the data items at the consumer site.

### Pushing or pulling
Delivery of data from producer to consumer can take place in two ways:
Pushing: If the producer/sender delivers data whenever it is produced, without
a prior request from the consumer/receiver.
Pulling: If the producer delivers data only when the receiver first requests them.
![[Pasted image 20231031133719.png]]
When the producer pushes the items, the consumer may be overwhelmed and there
is a need for flow control, in the opposite direction, to prevent discarding of the items.
However, there is no need for flow control when the consumer pulls the items (since it
requests when it is ready).

### Roles of the layers
When we deal with communication at the transport layer, we are dealing with four entities:
• Sender process
• Sender transport layer
• Receiver process
• Receiver transport layer

The sender process at the application layer is only a producer. It produces messages and passes them on to the transport layer.

The sender transport layer has a dual role:
• It is consumer - packets are received from sender application layer through pushing.
• It is producer – packets are encapsulated and sent to the receiver transport layer
through pushing.

The receiver transport layer also has a dual role:
• It is consumer – packets received from the sender transport Layer through pushing.
• It is producer – packets are decapsulated and delivered to the receiver application layer
through pulling.
![[Pasted image 20231031134018.png]]

### Buffers
Although flow control can be implemented in several ways, two buffers will often be used:
• One at the sender transport layer.
• One at the receiver transport layer.
• When the buffer at the sender transport layer is full, the application layer is informed
to stop delivering messages.
• When the buffer has some vacancies, the application layer is informed that it can
continue the delivery of messages.
• When the buffer at the receiver transport layer is full, the sender transport layer is
informed to stop delivering messages.
• When the buffer has some vacancies, the sender transport Layer is informed that it
can continue the delivery of messages.
One could implement one ring-buffer (on the sender and receiver sides) for this flow
control.

## Error control
Since the network layer is unreliable (IP protocol), we need to make the transport layer
reliable if an application requires reliability.
This reliability can be e.g., achieved by adding an error control service to the transport layer.
Error control at transport layer's level is responsible for:
1. Detecting and discard corrupted packets.
2. Keeping track of lost and discarded packets and resending them.
3. Recognizing duplicate packets and discarding them.
4. Buffering out-of-order packets until the missing packets arrive.
Error control only involve the sender and receiver transport layers
(as opposed to the flow control we just looked at)
![[Pasted image 20231031134341.png]]

### Sequence numbers
Error control requires that:
• The sender transport layer knows which packets is to be resent.
• The receiver transport layer knows which packet is a duplicate, or which packet has
	arrived out of order.
This can be done if the packets are numbered!
We add a sequence number in a field in the transport layer packet.
With this sequence number, the above error control can be performed.
• The packet numbering takes place sequentially (i.e., consecutively).
• The sequence number field sets a limit on the size of the sequence numbers.
• When the maximum number is reached, we can wrap around the sequence. (the
sequence numbers are modulo $2^m$ and m is the number of the bits in the field.)

### Acknowledgment
• The receiver can send receipts (ACK) back to the sender when error-free packets
	are received.
• The sender starts a timer when a packet is sent. If the sender does not receive this
	receipt before the timer expires, the packet will be resent.
• If the receiver had sent a receipt that did not arrive in time, the receiver will receive
	the resent duplicate package (which can be just discarded silently based on the
	sequence number by the receiver)

### Combination of Flow and Error Control
Sequence numbering and acknowledgement can be combined if we use two numbered
buffers on the sender and receiver sides, which place packets in the buffer in relation to
the sequence number.

### Example of implementation: Sliding window
Since the sequence numbers use modulo $2^m$ , a circle can represent sequence numbers
from 0 to $2^m–1$. The buffer is represented as a set of slices, called sliding window, that
occupies part of the circle at any time.
![[Pasted image 20231031135023.png]]
• The leftmost packets are acknowledged (12 - 15), the sender no longer has copies of them. They are finished.
• The packets in the shaded field of the window, the sender needs to have copies of them, as they have been sent, but their fate is not known yet, we do not know if they should be resent or not.
• The white packets in the window are ready to be sent, but data has not yet been handed over to the network layer.

## Congestion control
• An important issue in a packet-switched network, such as Internet, is Congestion.
• This occurs when the number of packets (the load) sent to the network is greater than the capacity of the network.
• Congestion control refers to a mechanism/technique that controls congestion and keeps the load below capacity.

Congestion in a network occurs because routers and switches have queues--buffers that hold the packets before and after processing. Congestion at the transport layer is actually the result of congestion at the network layer, which manifests itself at the transport layer.
Later we will see how the TCP protocol (assuming that there is no congestion control at
the network layer) makes its own congestion control mechanism.

## Connectionless Service
In a Connectionless service, packets are sent without the need of establishing a logical connection at the beginning and closing it in the end.
• Packets are not numbered,
• or can be lost,
• or arrive at the receiver ”out‐of‐order”,
• There is no receipt for received packets,
• UDP protocol is an example of such a "Connectionless service".
This means that the transfer of data can happen very fast, as there is almost no overhead on the operations, but the connection is not as stable.

### Example
![[Pasted image 20231031135637.png]]

## Connection-oriented service
In a Connection‐oriented service, there must be:
• first, a logical connection is established between sender and receiver,
• Then data is sent,
• and the logical connection is closed in the end.
• TCP and SCTP are examples of ”Connection‐oriented service”.
This is a more reliable connection, but is slower than connectionless.

### Example
![[Pasted image 20231031135710.png]]