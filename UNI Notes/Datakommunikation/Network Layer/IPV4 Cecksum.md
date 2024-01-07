>Its used to see if the header is corrupted

IPv4 checksum is performed as follows:
* The checksum is initialized to 0.
* The entire IPv4 header is divided into 16-bit sections/words.
* All these sections are added together.
* The resulting sum is complemented.
* This value is inserted into the header.

The checksum in an IPv4 datagram includes only the header, not data!

There are two reasons for this:
* All upper-level protocols have their own checksum field that covers the data they encapsulate into an IPv4 datagram.
* Since the header in an IPv4 datagram changes every time it passes a router, and if the data (payload), which does not change, was also included in the checksum, then the entire datagram had to be recalculated. Now you can just calculate the checksum for what is actually changed (the header).

***
#### Example
![[Pasted image 20231024131611.png]]
