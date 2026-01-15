![[Pasted image 20230922083532.png]]

## Semaphores
#semaphore
![[Pasted image 20230922084259.png]]
Atomic: The process is uninterruptible.
Wait(), is used to tell another process that it should not run its critical section, by making it wait for the s-variable to become zero.
Signal() is used to signal that the critical section is finished, and other processes can access their critical sections.
### Examples
![[Pasted image 20230922084635.png]]
Semaphore queue implementation:
![[Pasted image 20230922085231.png]]

With semaphores it is important to use the wait() function before entering the critical section, and use the signal() function when leaving the critical section. If this is not done, there will not be proper process synchronization.
## Monitors
![[Pasted image 20230922090051.png]]
Processes within a monitor are mutually exclusive, meaning that only one at a time can ever modify their shared data at any one time.
This is however inefficient, as not all processes need to be mutually exclusive.
![[Pasted image 20230922090257.png]]
To solve this inefficiency, condition variables are introduced in to the monitor, which basically have the same behavior as the semaphores, effectively combining the two synchronization strategies.

## Deadlocks
![[Pasted image 20230922091555.png]]

## Synchronization problem examples
### Bounded-buffer problem
#bounded #buffer #boundedbuffer
![[Pasted image 20230922091929.png]]
The mutex variable is used to ensure that only one of the processes are modifying the variables at a time. The variables empty and full are used to monitor whether there is new data to read and if there is space to write new data in the buffer.
![[Pasted image 20230922092128.png]]
![[Pasted image 20230922092140.png]]
### Readers-Writers problem
#readers #writers #readerswriters
![[Pasted image 20230922092522.png]]
![[Pasted image 20230922092719.png]]
![[Pasted image 20230922092814.png]]
When there are one or more readers, reading the database, the writers are not allowed to write new data.
### The Dining-Philosophers Problem
#Dining #Philosophers #Diningphilosophers
![[Pasted image 20230922093246.png]]
#### Semaphore solution
![[Pasted image 20230922093258.png]]
![[Pasted image 20230922093349.png]]
#### Monitor solution
![[Pasted image 20230922093555.png]]
![[Pasted image 20230922093627.png]]
![[Pasted image 20230922093648.png]]
