![[Pasted image 20231026203207.png]]

## System calls
Functions that are provided by the operating system, to accomplish basic tasks, such as reading and writing files, writing output to the screen, and provide I/O operations.
![[Pasted image 20231026203931.png]]

### API
![[Pasted image 20231026203514.png]]
### Parameters transfer
Parameters can be transferred both directly from the function to the system call, or by loading the parameter to a register, and loading it from there.

## Processes
A proces is a program that has been loaded in to memory. The operating system will store various information about the proces, to best allocate it's resources between various processes. This information can also be used to interrupt a proces, save it's state, and return to it at a later time. The memory in which this information is stores is called a Process Control Block (PCB).

### Interprocess communication models
![[Pasted image 20231026204655.png]]
The message passing method has the advantage, that the processes are not trying to read or edit the same memory, but it is slower, due to the communication having to happen through the kernel. 
The shared memory method is faster, as the processes can access the same memory, but you have to make safeguards to avoid that the processes try to edit the same memory at the same time.

