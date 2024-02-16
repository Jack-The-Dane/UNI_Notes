When nodes are connected in a common link, also called a multipoint
or broadcast link, then we need to have a protocol that can handle and
coordinate access to the link.
The problem is handled by the protocols similar to the rules of speaking
in an assembly:
• The right to speak is maintained.
• It is ensured that two people do not speak at the same time.
• It is ensured that they do not interrupt each other.
• It is ensured that the conversation does not develop into a
monologue (i.e., only one gets speaking time)
• And so on

![[Pasted image 20231003122201.png]]
## Random access
Random Access means:
• that no nodes are more important than others,
• that no nodes are assigned control over others,
• that no nodes allow or forbid others to send,
• that all nodes send whenever they want, provided that they follow
some predefined procedure, which includes testing the state of the
medium (busy/idle).

Since all nodes can send whenever they want, access conflict can occur,
also called collision.
The involved frames will either be destroyed or modified.
To avoid this or solve the problem when it happens, all nodes follow
procedures that answer the following questions:
• When can a station access the medium?
• What can a station do if the medium is busy?
• How can a station determine a successful or faulty transmission?
• What can a station do if there is an access conflict?

### Pure ALOHA 
![[Pasted image 20231003122838.png]]
In Pure ALOHA, the station transmitting a frame expects an ACK from the receiver
once it has received the frame successfully.
If the sender has not received an ACK before a timeout. Then it assumes that
frame has been lost and resends it.
If all the stations involved in a collision try to resend after a timeout, then the
collision happens again.
Pure ALOHA therefore dictates that: When the timeout period is over, each
station waits for another random time period before resending.
We call this random time period Backoff time TB.
Pure ALOHA has another method to prevent the channel (medium) from being
flooded with retransmitted frames. After a maximum number of retransmission
attempts KMAX, the station gives up and tries again later.
![[Pasted image 20231003122910.png]]
![[Pasted image 20231003122933.png]]
#### Throughput of Pure ALOHA
$$S = G \cdot e^{-2G}$$
Where **G** is the average number of fames generated during a frame
transmission time $T_{fr}$
_Throughput_ is the percentage of the frames which can reach their destination
successfully.
At max throughput, **G=0.5,** as the vulnerable time is $2 \cdot T_{fr}$. Which
gives $S_{max} =0,184$ or
**18,4% of the sent frames arrive without error.**

### Slotted ALOHA
![[Pasted image 20231003123259.png]]
![[Pasted image 20231003123346.png]]
$$S=G \cdot e^{-G}$$
At max throughput, $G=1$, as the most vulnerable time is $T_{fr}$. Which gives $S_{max}=0,368$ or
36,8% of the sent frames arrive without error.

### Carrier Sense Multiple Access (CSMA)
The risk of collision can be reduced if the station examines the medium before
attempting to use it.
The principle is called “sense before transmit” or “listen before talk”.
![[Pasted image 20231003123603.png]]
![[Pasted image 20231003123637.png]]
If one station transmits and another station starts a transmission within this
time period ($T_P$) after the start of the first station’s transmission, then a
collision is very likely to happen.

#### Persistent methods
What should a station do if the channel is busy?
what should a station do if the channel is free?
3 methods have been developed to answer these questions:
**• 1-persistent method
• Nonpersistent method
• p-persistent method**

##### 1-persistent method 
This is the simplest. Measure all the time until the
medium is free, then send.
This method has the highest risk of collision among the three methods.
Ethernet uses this method.
![[Pasted image 20231003123849.png]]

##### Nonpersistent method
A station has a frame to send. If the channel is free, it
sends immediately. If the channel is busy, it waits a random amount of time
and then sense the channel again.
This reduces the risk of collision (compared to the first method).
![[Pasted image 20231003123957.png]]

##### P-persistent method
This method is used if the channel is divided into
time slots whose length is greater than or equal to the propagation time.
This method combines the advantagesof the two previous methods. This
reduces the risk of collisions and improves efficiency.
![[Pasted image 20231003124032.png]]

### Carrier Sense Multiple Access with Collision Detection (CSMA/CD)
• CSMA does not specify what to do if a collision occurs.
• CSMA/CD describes an collision handling algorithm.
To better understand CSMA/CD, let's look at the first bit transmitted by
two stations involved in a collision…
![[Pasted image 20231003124439.png]]
![[Pasted image 20231003124713.png]]
![[Pasted image 20231003124801.png]]
#### Flowchart CSMA/CD
![[Pasted image 20231003125000.png]]
#### Energy levels
![[Pasted image 20231003125030.png]]
#### Throughput
The throughput at CSMA/CD is greater than at both Pure ALOHA and Slotted ALOHA.
The throughput obviously depends on the value of the G value
(and the p-value if the p-persistent method is used)
• For 1-persistent method, the throughput is approx. 50% (at G=1)
• For non-persistent method up to 90% (at G between 3 and 8)

### Carrier Sense Multiple Access with Collision Avoidance (CSMA/CA)
As we saw, collisions could be detected by energy measurement.
It is also easy enough in a wired system, where the energy is doubled in
the event of a collision.
But in a wireless system, much of the energy is lost in the transmission itself. Therefore, a collision may add only 5-10% extra energy.
This provides no effective way to detect collisions.
We must therefore avoid collisions in a wireless network because they can be difficult to detect.

**Collisions are avoided using CSMA/CA's 3 strategies:**
• Interframe space
• Contention window
• Acknowledgment

![[Pasted image 20231003125320.png]]

#### InterFrame Space (IFS)
Collision is initially avoided by delaying the transmission even if the
channel is found idle.
The station does not transmit immediately. It awaits a period called
Interframe Space (IFS).
If the channel is still available after IFS, then the station is almost
ready to transmit. It must first go through the Contention time
(corresponding to the contention window).
The time for IFS can be used to make priority, the shorter the time the
higher the priority, and conversely the longer the time the lower the
priority. This can apply to either the station or the importance of the
transmitted frame.

#### Contention Window
This window consists of a certain amount of time, which is divided into slots.
When a station is ready to send, it waits a random number of slots before
it starts sending.
The waiting time changes according to the binary exponential Backoff
strategy.
This means that the maximum value of the slot number is doubled every
time the station cannot detect an idle channel after the IFS time.
(this is very similar to the p-persistent method).
Note that the station needs to sense the channel after each time slot:
If the channel is busy, the timer is stopped until the channel is idle again.
Then continue with the next time slot until the set number of time slots is
expected.

#### Acknowledgements
Even though we have all these precautions, collisions can still occur which can corrupt our data.
Therefore, an ACK and a time-out timer should help guarantee that the receiver has received the frame correctly.
#### Flow diagram
![[Pasted image 20231003125635.png]]
#### Example
1. Before sending a frame, the source station senses the medium by checking the energy level at the carrier frequency.
	a. The channel uses a persistent strategy with "backoff" until the channel is idle
	b. When the channel is found idle. The sender is waiting for a time called DCF interfarme space (DIFS). Then a control frame, Request To Send (RTS), is sent
2. After receiving RTS and waiting for a period called short interframe space (SIFS), the receiver sends a control frame: Clear To Send (CTS) to indicate that it is ready to receive data.
3. The sender sends data (after a SIFS period)
4. The receiver sends a receipt ACK. Note that this is necessary as the stations cannot use collision detection in CSMA/CD 
	(only 5-10% extra energy is added in the carrier)
![[Pasted image 20231003130134.png]]
A few things to note:
• Since there is no collision detection, collisions can occur during the handshaking
period if several stations send an RTS and do not receive a CTS (due to collision).
Then the "backoff" strategy (random pause) is used before RTS is sent again.

• In the figure, there is a field called NAV = Network Allocation Vector.
Both RTS and CTS indicate the value of NAV in their control frame.
The value is the duration of the time the channel is occupied by data
traffic between sender and receiver.

• We can see that a RTS-frame cannot reach C and D. That is why both
RTS- and CTS-frames contain the value NAV.
All stations that are not involved in the communication (here C and D) start a
timer with the value of NAV to first check if it has expired before sensing the
physical medium again.

## Controlled Access
### Reservation 
According to this method, a station must make a reservation before data can be transmitted. The time is divided into intervals. In each interval, a reservation frame is sent before data frames are sent.
• If there are N stations in the system, then there are also N mini-slots in the reservation frame.
• Each mini-slot belongs to a specific station.
• When a station wants to send, it makes a reservation in its own mini-slot.
• The stations that have reserved transmission time can transmit their data frames after
reservation frame.
![[Pasted image 20231003130350.png]]
### Polling
Polling works with topologies, in which one station is designated as the primary
station and other devices are secondary stations. All data exchange must take
place through the primary station.
• The primary station controls the link.
• The secondary station follows the instructions of the primary station.
• It is up to the primary station to decide who is allowed to use the channel at a given time.
• The primary station is always the initiator of a session.
2 functions are used.
#### Select (SEL)
This function is used when the primary station has something to send.
Remember that the primary station controls the link.
• First, SEL is sent and an ACK is awaited.
• Then data is sent and an ACK is awaited.
![[Pasted image 20231003130509.png]]

#### Poll
This function is used by the primary station when it wants to request transmission from
the secondary station.
When the primary station is ready to receive data, it (polls) asks the secondary stations in
turn if they have anything to send.
• If a secondary station has nothing to transmit, it sends a NAK.
• If a secondary station has something to send, it sends its data and waits for an ACK.
![[Pasted image 20231003130540.png]]

### Token passing
In this method, the stations are organized in a logical ring. In other words, there is a predecessor and a successor to each station in the network.
• The station that has the token right now also has access to the channel.
• When the current station has no more to send, it passes the token on to its successor.

How is such a token passed on to the next station?
• In this method, a special packet (token) circulates around the ring.
• When a station has some data to send, it waits until it receives the token from its predecessor.
• When it receives the token, it sends its data.
• It then passes the token on to its successor when it has no more data to send.

However, some overall management is needed in connection with the token:
• The time a station can have a token must be limited.
• The token must be monitored to ensure that it is not lost or destroyed.
• Priority must be given to stations and types of data that are transmitted.
• A low priority station should only be forced to hand over the token to a higher priority station.

#### Examples of logical ring topology
![[Pasted image 20231003130944.png]]

## Channelization
### Channel Partition
Channel partition is a multi-access method where the available bandwidth of a link is shared in:
• Frequency
• Time
• Through coding
… among different stations

### Frequence-Division Multiple Access (FDMA)
Here the bandwidth is divided into frequency bands. Each station is allocated to a frequency
band where it can transmit its data. This frequency band belongs to the station at all times.
To avoid interference, the frequency bands are separated by a narrow _Guard_ band.
![[Pasted image 20231003132231.png]]

### Time-Division Multiple Access (TDMA)
Here the bandwidth in the link is divided in time. Each station has its own time slot in
which it can send data. The data stream is divided into packets.
![[Pasted image 20231003132314.png]]
The main problem with TDMA lies in achieving synchronization between the individual stations.
• Each station must know when its time slot starts.
• This can be difficult if the stations are spread over a larger area, because then propagation delays must also be taken into account.
• However, we can compensate for this by inserting guard times between the time slots.
• Synchronization is usually achieved by having some synchronization bits at the beginning of each time slot.
### Code-Division Multiple Access (CDMA)
The idea for CDMA was conceived decades ago, but recent advances in electronic technology have finally made its implementation possible.
• CDMA differs from FDMA because only one channel has the full bandwidth of the link.
• CDMA differs from TDMA because all stations can broadcast simultaneously. There is no timesharing.

Let us assume that 4 stations 1, 2, 3 and 4 are connected to the same channel.
• Data from station 1 is d1, data from station 2 is d2 and so on
• The code associated with station 1 is c1, the code associated with station 2 is c2 and so on
We assume the associated codes have two properties.
1. If we multiply one code by another, we get the result 0.
2. If we multiply a code by itself, then we get the number of stations (here 4)

#### Example
![[Pasted image 20231003132634.png]]
Station 1 and 2 communicate with each other. Station 2 want to see what station 1 is
broadcasting. Therefore, station 2 multiplies the data on the channel with station 1’s
code c1.
![[Pasted image 20231003132844.png]]
then, by dividing by 4, station 2 will be able to find out what station 1 has sent.

#### Chip Sequences
![[Pasted image 20231003133006.png]]

#### Data Representation
• A bit that is 0 is presented as -1
• A bit that is 1 is presented as +1
• If nothing is sent, it is presented as 0

#### Example
![[Pasted image 20231003133120.png]]
![[Pasted image 20231003133204.png]]
![[Pasted image 20231003133234.png]]
#### Generation of chip sequence (Walsh tables)
![[Pasted image 20231003133407.png]]
