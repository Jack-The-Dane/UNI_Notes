In addition to error reporting, ICMP can diagnose some network issues. This is achieved via inquiry messages. There are 4 different sets of queries.
![[Pasted image 20231024135335.png]]

***
**Echo request (type 8) and echo reply (type 0):** this pair of messages are used by a host or a router to test the liveliness of another host or router. A host or router sends an echo request message to another host or router; if the latter is alive, it responds with an echo reply message. 

Echo request and reply can help determine if there is any communication at the IP level. It also shows that intermediate routers that forward the IP datagram, are working. 

***
**Timestamp request (type 13) and reply (type 14):** Two nodes (hosts or routers) can use this request/reply to determine the round-trip time for an IP datagram traveling between them.
It can also be used to synchronize the local clocks in the two nodes.

***
>the message is categorized as obsolete by the IETF (Internet Engineering Task Force)

Address mask: Type 17 and 18: A host may know its IP address, but not the corresponding mask.
E.g., if the host has the address 159.31.17.24, but does not know the corresponding mask (e.g., /24).
* To find out his mask, the host sends a request (type 17) to a router on his LAN.
* If the host knows the router's IP address, then the message is sent as unicast, otherwise it is sent as a broardcast.
* The router sends a reply (type 18), with information about the host's mask.
* The mask can be used together with the IP address to determine the address of the subnet. (as we have seen)

***
Router solicitation and advertisement: Type 10 and 9: As we have seen before, in connectionwith "redirection", a host that wants to send an IP packet to another host on another LAN, know the address of a suitable router..

The host must also know if the router is "alive" and working properly. Here, this type of request /reply can help.
* The host can be type 10 broadcast. (broardcast can, as we remember, only take place on the LAN).
* The routers that receive this request broardcast their routings information, that is, type 9.

Alternatively, a router may also periodically broadcast (advertise type 9) its information, even if no host has requested (type 10) to do so.