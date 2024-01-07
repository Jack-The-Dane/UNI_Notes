## IEEE Standards
![[Pasted image 20231003133757.png]]

### Standard Ethernet
Originally, The Ethernet LAN was developed in the 1970s by Robert Metcalfe and David
Boggs. Since then, it has gone through four generations as the demands for higher data rate
have been increasing, we will look at 3 of them:
![[Pasted image 20231003133847.png]]
#### Frame format for MAC-frame
• Ethernet has no mechanisms to acknowledge received frames.
• Therefore, it is considered an unreliable medium.
• If a receipt is to be received for received frames, it must be implemented in higher layers.
![[Pasted image 20231003133922.png]]

**Preamble:** This field consists of 7 bytes (56 bits) of alternating 0s and 1s.
The field is used to alert the receiver to the coming frame and allows the
receiver to synchronize its clock with the sender.
In fact, this field is actually added at the physical layer and is therefore
not officially part of the frame.

**Start frame delimiter (SFD):** This field has 1 byte and contains a constant value
10101011. It signals the start of a frame. The receiver is warned that this is the
last chance to get ready to receive the coming frame.
This field is also added at the physical Layer.

**Destination address (DA):** This field has 6 bytes and contains the link-layer address
of the destination station or stations, i.e.,receiver(s).

**Source address (SA):** This field has 6 bytes and contains the link-layer address of
the sender of the packet.

**Length or Type:** The standard Ethernet uses this field for type indication, while IEEE uses the field to specify the number of bytes in the data field.
Both statements are common today.
If type is used, this value is larger than 1536 (0x0600) and indicates the upper-layer protocol whose packet is encapsulated in the frame. Here, interpackets gap (which is the distance between frames = 12 byte) is used to detect the frame length.
E.g.: 0x0806 = ARP and 0x86DD = IPv6

**Data and padding:** This field contains data encapsulated from the upper layers. The size is between
46 and 1500 bytes.
If data in this field is less than 46 bytes, then 0s are inserted (padding).

**CRC:** This field contains error detection information, in this case CRC-32.

#### Frame length
Ethernet has restrictions on both the minimum and maximum lengths of a frame.
![[Pasted image 20231003134258.png]]
The minimum length is a requirement for the proper functioning of CSMA/CD. It is set to be at least 512 bits or 64 bytes.
The reason is that the transmission time for a frame (Tfr) must be at least 2xTp (propagation) for collision detection.
If the upper layer delivers less than 46 bytes to the MAC layer, then some padding is conducted to fit.

The maximum limit has two historical reasons.
• In the early days of Ethernet, memory was very expensive. By limiting the size, one could also limit the size of buffers.
• The maximum limit should help ensure that a station does not monopolize the shared medium for too long at a time.

#### Addressing
Each station on an Ethernet network (such as a PC, workstation, or
printer) has its own Network Interface Card (NIC). The NIC fits inside the
station and provides the station with a link-layer address. The Ethernet
address is 6 bytes (48 bits), normally written in hexadecimal notation,
with a colon between the bytes.
![[Pasted image 20231003134436.png]]

#### Unicast Multicast and Broadcast addresses
A source address is always a unicast address, the frame only comes from one
station. But the destination address can be unicast, multicast or broadcast
addresses.
• If the least significant bit (lsb) in the first byte is 0, then it is a unicast address.
• If the lsb in the first byte is 1, then it is a multicast address.
• If all bits in the address are 1 (FF:FF:FF:FF:FF:FF), then it is a broadcast address.
![[Pasted image 20231003134526.png]]

#### Access Method
Standard Ethernet uses CSMA/CD with 1-persistent method.

#### Slot time
The slot time is referred to as the time it takes to send 512 bits.
This means that the slot time depends on the data rate.
For traditional 10-Mbps Ethernet, the slot time is 51,2 µs.

#### Slot time and collision detection
The choice of a 512-bit slot time is not random. It is selected for CSMA/CD to work properly.
In Ethernet, roundtrip time is the time it takes for a frame to be transmitted from one
end of a network to the other and back again.
$$Slot\; time = roundtrip\; time$$
This is equivalent to two nodes (A and B) furthest apart in a network doing the
following:
• Node A transmits 512 bit.
• Just before the first of the 512 bits arrives at node B, B also sends 512 bits.
• When B’s first bit arrives at A, then A must not have sent its last bit.
Remember A and B only do collision detection while transmitting!
![[Pasted image 20231003134918.png]]

There is a relationship between the slot time and the maximum length of a
network (the collision domain).
It depends on the propagation rate. In most transmission media, signals move at a
speed of 2x108 m/s (equivalent to 2/3 of the propagation rate in air).
We can thus calculate:
$$\text{Max Length} = \text{Propagation rate} \cdot \frac{\text{Slot time}}{2}$$
$$\text{Max Length} = 2 \cdot 10⁸ \cdot \frac{51.2 \cdot 10^{-6}}{2} = 5120\ m$$
However, we should also consider delays in repeaters and interfaces, as well as the time
required to send jam signals. These circumstances in practice reduce the maximum length
to 2500 m (48% of the theoretical value).

#### Physical layer
![[Pasted image 20231003135257.png]]
![[Pasted image 20231003135311.png]]

##### 10Base5: Thick Ethernet
![[Pasted image 20231003135352.png]]

##### 10Base2: Thin Ethernet
![[Pasted image 20231003135413.png]]

##### 10Base-T: Twisted-pair Ethernet
![[Pasted image 20231003135444.png]]

##### 10Base-F: Fiber Ethernet
![[Pasted image 20231003135513.png]]

##### Summary
![[Pasted image 20231003135533.png]]

## Changes in standard
### Bridged Ethernet
![[Pasted image 20231003135830.png]]

### Switched Ethernet
![[Pasted image 20231003135854.png]]

### Full-Duplex Switched Ethernet
![[Pasted image 20231003135941.png]]

### MAC Control
Since standard Ethernet was designed as a connectionless protocol without
Flow- and Error-control. Then it was necessary to add a layer in between the
LLC layer and the MAC layer that could handle these controls. This layer is
called **MAC Control Layer.**

## Fast Ethernet
Fast Ethernet was designed to compete with other high-speed LAN protocols. IEEE created Fast Ethernet as standard 802.3u.
Fast Ethernet is backward compatible with Standard Ethernet, but the speed is
10 times higher with a data rate of 100 Mbps.
The following goals for Fast Ethernet can be summarized:
1. Upgrade the speed to 100 Mbps.
2. Make it compatible with Standard Ethernet.
3. Keep the same 48-bit MAC address.
4. Keep the same Frame format.
5. Maintain the same minimum and maximum lengths for frames.

### Autonegotiation
A new feature is added and called Autonegotiation (automatic negotiation)
The purpose is as follows:
• Allow incompatible devices to connect to each other. E.g., 10Mbps device can communicate with 100Mbps device.
• Allow one device to have multiple capabilities.
• Allow a station to check the capabilities of a hub.

### Physical Layer
The physical layer of Fast Ethernet is more complex than Standard Ethernet. Two stations can be connected as Point-To-Point and three or more stations need to be connected in star topology (with a hub or switch in the middle).
![[Pasted image 20231003140341.png]]

### Encoding
If you want to do Manchester coding for data speed of 100Mbps, then it
requires a bandwidth of 200 Mbaud.
This makes Manchester coding unusable for twisted-pair cables, which do not have such high bandwidth.
Fast Ethernet designers sought some alternative encoding/decoding scheme. Three different encoding schemes were chosen for three different implementations.

####  3 Methods of encoding
![[Pasted image 20231003140503.png]]

### Summary
![[Pasted image 20231003140556.png]]

## Gigabit Ethernet
The need for even faster data speeds led to the design of the Gigabit Ethernet protocol. IEEE has given it the name standard 802.3z.
The following Gigabit Ethernet targets can be summarized:
1. Upgrade the speed to 1 Gbps.
2. Make it compatible with Standard and Fast Ethernet.
3. use the same 48-bit MAC address.
4. Keep the same frame format.
5. Maintain the same minimum and maximum lengths for Frames.
6. Support autonegotiation as defined in Fast Ethernet.

### MAC Sublayer
One of the main considerations in the development of Gigabit Ethernet was to keep the MAC sublayer untouched.
But this was no longer possible if one wanted to achieve 1Gbps.
Gigabit Ethernet has two distinctive approaches for medium access:
• Half-duplex.
• Full-duplex.

#### Full-Duplex mode
• In Full-duplex, there is a central switch, which is connected to all stations or switches.
• Here, each switch has a buffer in all input ports, which holds data until it is sent.
• Since the switch divides the collision domain into N domains, there are no
collisions, therefore CDMA/CD is not used.
• This means that the length of the cables is determined by the attenuation of the
cables, and not by the collision detection algorithm (CD).

#### Half-Duplex mode
3 methods are defined:
• Traditional
• Carrier Extention
• Frame Bursting.

**Traditional:** here the same minimum length is used on the frame as in traditional
Ethernet (512bit). But since the length of a bit is 1/100 shorter in Gigabit Ethernet
than in traditional Ethernet (10Mbps), the slot time is reduced to 0.512µs, which
means that collision is detected 100 times earlier, which in turn means that the
cable length can only be 25 m.

**Carrier Extention:** to allow a longer (larger) network, we increase the minimum
length of a frame. Here, the minimum frame length is defined as 512 bytes = 4096
bit. This means that the minimum length is increased 8 times. This also increases
the cable length 8 times to 200 m (100 m from station to hub).
If less than 4096 bit is to be transmitted, bit padding is used.

**Frame Bursting:** Carrier Extension is very inefficient if only short messages (bit
padding and redundant bits) are sent.
Instead of adding extension to each frame, more frames are sent.
But to make these multiple frames look like a frame, bit-padding is added in
between the frames.
This makes the many frames look like one, and since the medium is not idle
between the frames, other stations are deceived into thinking that only a very
large frame has been transmitted.

### Physical layer
Two stations can be connected in Point-To-Point.
Three or more stations are connected in star, with a switch or hub in the center.
![[Pasted image 20231003141250.png]]

Gigabit Ethernet can be categorized as either two-wire or four-wire
implementation.
• Two-wire: Fiber-optic cable: 1000Base-SX (short-wave), 1000Base-LX (long-wave), copper cable: 1000Base-CX (STP).
• Four-wire: 1000Base-T (Category 5 UTP)
![[Pasted image 20231003141335.png]]
#### Encoding
![[Pasted image 20231003141407.png]]

### Summary 
![[Pasted image 20231003141459.png]]
