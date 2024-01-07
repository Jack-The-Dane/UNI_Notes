## 8-Bit
### General 8-bit Interface with full hardwired address decoding
![[Pasted image 20231103082307.png]]

### RAM (Random Access Memory)
The RAM chipset will only be active when no signal is entering the /CS pin. The NAND gate regulates the activation of this chipset, which means that the chipset will be selected when all the pins A12-A15 are 1.
This practically puts the RAM block to the top of the memory space.

### ROM (Read Only Memory)
The ROM chipset will only be active when no signal is entering the /CS pin. The OR gate regulates the activation of the chipset, which means that the chipset will be selected when all the pins A8-A15 must be 0.
This practically puts the ROM block to the bottom of the memory space.

Whether the memory is read from or written to is decided by the /RD and /WR pins, respectively.

![[Pasted image 20231103083342.png]]

## 16-Bit
### General 16-bit Interface with full hardwired address decoding
![[Pasted image 20231103083426.png]]
![[Pasted image 20231103084243.png]]
A0 not being used, does not mean that you can only access every other address in each block. Because A1 is connected to the A0 of each block.

## Different interfaces
Many CPUs do not have separate address / data pins
This is caused by some historical reason at the early stage of the development when the number of physical pins on the CPU was limited.
Nowadays, most manufacturers still offer this interface for compatibility reasons.
![[Pasted image 20231103084516.png]]

## Wait state
Some chipsets, e.g., EPROM may require additional time to fetch the necessary data, for which a
wait-state generator can be implemented.
![[Pasted image 20231103084858.png]]
Notice that it is the CS signal that starts the wait-state generator.
8284 is the wait-state generator
8088, 8086 is the CPU

### Example, No wait state
![[Pasted image 20231103085435.png]]

### Example, 1 wait state
![[Pasted image 20231103085519.png]]
