Although IP security is not part of this course, we will still briefly look at some security issues in the IP protocol and the corresponding solutions that exist.
There are three issues that particularly applicable to IP protocol:
* Packet sniffing
* Package modification
* IP spoofing

***
#### Packet Sniffing
Packet sniffing is a passive attack where the attacker does not change the contents of the packets.

An intruder can intercept an IP packet and make a copy of it.
This type of attack is very difficult to detect as the sender and receiver will probably never discover that packets have been copied. 

Although packet sniffing cannot be stopped, encryption of the packet can make the attacker’s effort useless. The attacker may still sniff the packet, but the content is not detectable.

***
#### Packet Modification
This type of attack is more active.

Here, the attacker intercept the packets, changes their contents, and forwards the modified packets to the receiver. 

The receiver is deceived into believing that the packages come from the original sender. 

This type of attack can be detected using a data integrity mechanism. 

Before a receiver opens and uses the contents of the message, this mechanism is used to ensure that the packet has not been modified during transmission. 

***
#### IP Spoofing
An attacker could disguise himself as another person and create an IP packet that carries the source address of another computer. 

The attacker can e.g., send such IP packet to a bank and pretend to be one of the bank's customers. 

This type of attack can be avoided by using a source authentication mechanism.

***
#### IPsec
Today, IP packets can be protected from the above attacks by using the IPSec (IP Security) protocol.

This (IPSec) protocol, used in conjunction with the IP protocol, creates a connection- oriented service between two hosts, in which IP packets can be exchanged without having to worry about the attacks as described. 

IPSec adds the following services: 
* Algorithms and keys. Two hosts that want to establish a secure channel between them can agree to use available algorithms and keys for security purposes. 
* Packet encryption. The packets exchanged between two parties can be encrypted for privacy. This can be done with encryption algorithms and a shared key, which have been agreed in the first step. This makes packet sniffing useless. 
* Data integrity. Data integrity guarantees that packets have not been modified during the transmission. If a package does not pass a data integrity test, it will be discarded! This protects against packet modification attacks. 
* Source authentication. IPSec can authenticate the origin of the packet to be sure that the packet is not created by an imposter. This can prevent IP spoofing attacks.  