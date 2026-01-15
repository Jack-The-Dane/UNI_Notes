In the TCP/IP protocol suite there are three common transport layer protocols:
• User Datagram Protocol (UDP) which is:
	o Unreliable
	o Connectionless
This protocol is simple and efficient.
It is used by applications that can add error control (at the application layer level).
• Transmission Control Protocol (TCP) which is:
	o Reliable
	o Connection‐oriented.
This protocol can be used by all applications where reliability is important.
The application does not have to provide error control itself, (it is at Transport layer level)
• Stream Control Transmission Protocol (SCTP) which is a reliable and connection-
oriented.
	A new protocol that combines the good features of UDP and TCP.

# UDP protocol
This protocol is characterized as follows:
• Connectionless
• Unreliable communication
It does not really add any extra functionality compared to the IP protocol.
However, it offers process-to-process communication instead of host-to-host communication. There is also a very limited error control (through checksum).
Do you want to use UDP even though it is so limited? The answer is YES!
UDP is simple, it generates a minimum of overhead.
It requires less sender-receiver interaction than TCP or SCTP.

## Service
**Process-to-process communication:** UDP adds process-to-process communication. Here, the so-called socket address is used, which is a combination of IP address and port address.

**Connectionless Service:** UDP offers a connectionless service. This means that each user datagram sent via UDP is independent. There is no connection, even if they come from the same source process. The datagrams are not numbered, and no connection is established between sender and receiver before datagrams are sent.

**Limitations**
Only processes that send short messages which are small enough to be in one
user datagram can use the UDP protocol.
Maximum space in datagram is:
65,507bytes (65,535 bytes – 8 bytes UDP header – 20 bytes IP header)

**Flow control:** UDP is a very simple protocol that does not offer flow control. If the process using UDP needs flow control, then it must take care of it itself.

**Error Control:** UDP offers no error control other than checksum. If an error is found via the checksum, the datagram is discarded. The sender will not be notified.
If the process using UDP needs error control, then it must take care of it itself.

**Checksum:** The UDP checksum is different from the one we used in IP and ICMP. Here we have three sections for the checksum calculation:
o Pseudoheader.
o UDP header.
o Data from the application layer.
## Headers
![[Pasted image 20231107132658.png]]
### Pseudoheaders
If the Pseudoheader was not included here, a UDP datagram could arrive without error.
• But if the IP header was corrupted, then the UDP datagram could have ended up
with a wrong host!
The 8-bit protocol field in the IP header is 17, which corresponds to UDP. This is important
as both TCP and UDP can use some of the same port numbers. Therefore, a Pseudoheader
is included, and a packet can also be discarded if this field is changed along the way.

### Checksum of headers example
![[Pasted image 20231107132928.png]]

## Queuing
• Queues are linked in UDP to each port.
• Most often, both an incoming and an outgoing queue are created, but in some cases only an incoming queue is created.
![[Pasted image 20231107133114.png]]
## Applications
Although UDP does not meet very many criteria for reliable transport, UDP protocol is still the preferred protocol in certain applications since reliability has its costs:
• Flow‐ and Error‐control = slower and more complex service (reliable).
• No Flow and Error-control = faster and simpler service (unreliable).
Applications that only send short queries and receive short answers can advantageously
use UDP. (with short queries and answers it is meant that they can be in one datagram)
e.g., DNS service uses UDP as transport protocol.
Lack of error control can sometimes be an advantage.
Error checking can in fact give rise to an unstable data flow, which can be inappropriate.
Sometimes it's more important to have a steady stream of data than to have
complete data. e.g. Skype or other real-time applications.

**Typical applications of UDP**
• UDP is well suited for processes that only need a simple
request/response communication.
UDP is not often used for FTP service which usually deal with bulk data.
• UDP is well suited to processes, with its own flow and error control
mechanisms. For example, the Trivial File Transfer Protocol (TFTP)
contains procedures for flow- and error-control, it will be easy to use UDP.
• UDP is well suited as a transport protocol for multicasting.
Multicasting capability is embedded into the UDP software, but not into the
TCP software.
• UDP is used for management processes. e.g., SNMP (Simple Network Management Protocol)
• UDP is used for some route updating protocols.
e.g., RIP (Routing Information Protocol)
• UDP is typically used for interactive real-time applications that cannot tolerate uneven data flow but are tolerant of losing a little data occasionally. (e.g., real-time robot control)

