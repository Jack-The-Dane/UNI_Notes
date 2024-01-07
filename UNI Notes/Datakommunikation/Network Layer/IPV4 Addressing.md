An IP-address (ver. 4), IPv4, used today is a 32-bit address.
This address defines a unique connection of a device (for example, router or computer) to the Internet.

Two different devices connected to the Internet cannot have the same addresses. If a device has *m* connections to the Internet, then it also needs to have *m* addresses.
A router is an example of such a device.

Everyone who wants to connect to the Internet must accept the IP addressing system.

Since a IPv4 address has 32-bit, it gives:
![[Pasted image 20231012102715.png]]

A 32-bit IPv4 address is hierarchical and divided into two parts: a prefix and a suffix.
![[Pasted image 20231012102746.png]]

***
#### Classful Addressing
Initially, a classification system was used when addresses had to be specified. IP addresses were divided into 5 classes: A, B, C, D and E.
Each of these classes occupied a portion of the address space.
Here, fixed prefixes were used, but in order to accommodate both small and large networks, 3 prefixes with fixed lengths are used: n = 8, n = 16 and n = 24.
![[Pasted image 20231012102851.png]]

One of the problems here was that the classification system divided each class into a fixed number of blocks with a fixed size. Since the addresses were not distributed properly, the Internet was faced with the problem of the addresses being rapidly used up, resulting in no
more addresses available for organizations and individuals (address depletion).
![[Pasted image 20231012102949.png]]
* Class A was far too large for almost all organizations. Too many unused addresses.
* Class B was also too large for most organizations. Too many unused addresses.
* Class C was too small for most organizations. Too few addresses.

>This classification leads to a consequence that too many available addresses were not used and wasted, which is the reason that the classful addressing has become obsolete.

***
#### Address block
In 1996, the Internet authorities announced a new architecture called classless addressing. In classless addressing, variable-length blocks are used that belong to no classes.
![[Pasted image 20231012103112.png]]
Address blocks When a small or large business needs to get access to the Internet, it is assigned a block of addresses.
The size of this block is determined by the type and size of the business.
* A private household may receive only a few addresses.
* A large company might get a few thousand addresses.
* An ISP (Internet Service Provider) may get 1000 or 100,000 addresses (based on the number of customers)

##### Restrictions
To simplify the handling of addresses, the Internet authorities have imposed 3 restrictions for classless address blocks:
1. An address block must have a set of continuous addresses.
2. The number of addresses in a block must be 2n (1, 2, 4,8,…)
3. The first address (in decimal) in the block must be divisible by the number of addresses in the block.
Internet Corporation for Assigned Names and Numbers (ICANN) is the authority for block allocation.

##### Example of Address Block
![[Pasted image 20231012103300.png]]

##### Prefix Length
Since the prefix length is not inherent in the classless addressing, we need to separately give the length of the prefix. In this case, the prefix length, n, is added to the address, separated by a slash. The notation is informally referred to as slash notation and formally as Classless InterDomain Routing or CIDR.
![[Pasted image 20231012103447.png]]

#### CIDR Example
![[Pasted image 20231012103519.png]]

![[Pasted image 20231012103539.png]]

![[Pasted image 20231012103547.png]]

***
