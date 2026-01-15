**The principle of locality**
• Approx. 90% of the running time is spent within approx. 10% of the codes.
There are 2 types of locality
	1. Temporal locality (time locality). If data/code is accessed by the CPU, there is a
	high probability that the same data/code will be accessed in the near future.
	Maybe within a few nanoseconds.
	2. Spatial locality (area locality). If data/code is accessed by the CPU,
	there is a high probability that other data/code that is physically
	located close to them will be accessed in the near future.

## L1 Cache
![[Pasted image 20231201093446.png]]
• The cache contains a copy of a small section of the main memory
• The cache can be accessed much faster (here 400MHz) than the memory
• Efficiency depends on construction and replacement policies

### Construction
The cache is divided into slots, which consist of a number of bytes, for example 32 bytes
![[Pasted image 20231201093613.png]]
**Data traffic:**
• Between CPU and cache takes place in bytes or words
• Between cache and memory takes place in slots (e.g., blocks of 32 bytes)
**Performance and cost:**
• Depends a lot on the chosen address mapping method
Via an example, we look at the basic ideas in the 3 most common methods

#### Example - structure
• Primary memory of 4 Gigabytes (this will equate to 232 bytes)
• Slot size of 32 bytes (this will equate to 25 bytes)
• Cache size 8192 slots (this will correspond to 213 slots)
Cache size (8192 x 32) = 262,144 bytes or 256 kB
Then we divide the memory into 227 blocks of 25 bytes.
• The memory is not divided in a physical way, but the cache
views the memory that way.
• The slot size is often between 16 and 64 bytes.

#### Examples - mapping methods
![[Pasted image 20231201093925.png]]
![[Pasted image 20231201094020.png]]
![[Pasted image 20231201094429.png]]
![[Pasted image 20231201094455.png]]

### Cache operations
![[Pasted image 20231201095615.png]]

### Design considerations
When establishing a cache, there are some parameters to consider
such as: cache size, slot size and associativity.
![[Pasted image 20231201100225.png]]

### Access time
![[Pasted image 20231201100247.png]]
