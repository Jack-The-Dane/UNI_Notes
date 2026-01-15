## Functionality
Works by triangulation. A user receives signals from 4 different GPS satelites. The user's phone has the trajectory of all GPS satelites, and can check their exact positions, with the timestamp received from each satelite. The distance from each satelite is then calculated using the time difference between sending and receiving the signal. You need 3 satelites to calculate the position, and then you need 1 more, because you dont have an accurate clock as a user.

### Pseudo range (Distance from user to satelite)
$$p_i = \vert r_i \vert + b_u \cdot c + \epsilon_i$$
where:
$r_i$ Is the length of the vector between user and satelite
$b_u$ is the bias of the user clock
$c$ Is the speed of light
$\epsilon_i$ is all other errors combined (much smaller than $b_u$)

### Pseudo random noise
Used to identify what satelite is emitting what signal. This noise is modulated on to the main data stream of the satelite.
C/A + P is modulated onto the random noise and contains data (the almanac among others). This is low priority data that takes a long time to transfer, and needs to be downloaded from one satelite without interruptions. This is why a GPS can take a long time to initialise, if it needs to download the almanac first. A phone will download the almanac from the internet, and can therefore initialise much quicker.

### Disturbances 
Atmospheric delay: The signal from the satelite bumps into molecules in the atmosphere, and is therefore moving slower than the speed of light. This is a major error in GPS positioning.

Geometry of the satelites: 
Dilution Of Precision, scalar value to describe how accurate the GPS signal is. Also comes for horisontal precision, vertical precision and time precision. The accuracy is determined largely by the geometry of the satelites.
## Availability
Not written
## Accuracy
### Frequencies
- L1: 1575 MHz
- L2: 1227 MHz
- L3: 1196 MHz
These frequencies were chosen to avoid attenuation by water in the atmosphere.
The same signal is transmitted on 3 frequencies, because you can better estimate the speed of the signal through the atmosphere that way.

### SPS (Standard Positioning System)
Works in the +- 15 meter range. Can be improved using DGPS.
### DGPS (Differential GPS)
Put up an antenna, to calculate the error on the satelites it can connect to. It can do this because the antenna already knows where it is. It transmits the error of the satelites to the user.
Precision of ~1 meter.
### RTK (Real time kinematics)
Can sample the L1 signal frequency to know exactly where the user is. Advanced electronics and maths. Can get down to a precision of ~2 cm with the necessary info.
RTK can be used estimate the attitude of a drone, because it is so accurate, if placed far enough away from each other.

## Interfacing

## Coordinate systems, projections, datums
### On the globe
- Latitude, from -90 degrees (south pole) to 90 degrees (north), 0 at equator
- Longitude, connects at the poles. Distance between longitude lines varies depending on the latitude.
This is complicated to use.
### A different system
#### UTM
Slice the earth like an orange, and lay them out flat. Don't try to convert between the two systems yourself.
Northing is the distance from equator and up north.
Easting is how far east of the false origin.
![[Pasted image 20250912103817.png]]
### Datums - World Geographical System 84 (WGS84)
Many different datums to increase accuracy in certain parts of the world. But every gps supports WGS84.
![[PXL_20250912_085539816.jpg]]

