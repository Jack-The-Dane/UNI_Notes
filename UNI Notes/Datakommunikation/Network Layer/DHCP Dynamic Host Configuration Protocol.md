- [ ] We have seen how ISPs can receive a large block of addresses from ICANN (Internet Corporation for Assigned Names and Numbers).
We have seen how smaller organizations can receive smaller blocks of addresses from ISPs.
After a block of addresses are assigned to an organization, the network administration can manually assign addresses to the individual hosts or routers.
This can be done manually or automatically. If the automatic method is used, then it is done with Dynamic Host Configuration Protocol (DHCP).

* DHCP is an application-layer program that works in the client-server paradigm and that helps [[TCP (Transmission Control Protocol)|TCP]]/IP at the network layer.
* DHCP has found widespread use in the Internet and is so popular that it is often called the plug-and-play protocol.
* DHCP is often used to assign permanent or temporary IP addresses to network users. (e.g., schools, etc.)

A computer connected to a network often needs the following information:
* Its IP address
* Network Prefix (or address mask)
* The address of the network’s default router (so that it can communicate with other networks)
* The address of a name server (so names can be used instead of IP addresses) DHCP can be used to collect the information.

***
#### DHCP Message Format
![[Pasted image 20231012104917.png]]
The server uses a number, called a magic cookie, the number is in the format of IP address and has the value 99.130.83.99.
When a client reads a DHCP message, it looks for that number.
If it exists, then it knows that the next 60 bytes are options. These options have the format:
* 1-byte tag-field
* 1-byte length-field
* a variable length value-field
If the tag-field has the value 53, then the value field will define one of 8 different packet types:
![[Pasted image 20231012104952.png]]

***
#### DHCP Example
![[Pasted image 20231012105025.png]]
![[Pasted image 20231012105046.png]]
![[Pasted image 20231012105053.png]]
![[Pasted image 20231012105056.png]]
![[Pasted image 20231012105105.png]]

***
#### State Diagram
Error control DHCP uses the services of [[UDP (User Datagram Protocol)|UDP]], which is not a reliable protocol!
To add error control, DHCP does the following:
* DHCP requires [[UDP (User Datagram Protocol)|UDP]] to use checksum, which is optional in UDP.
* The DHCP client applies a timer and re-transmission policy if it does not receive the DHCP reply to a request
![[Pasted image 20231012105205.png]]
