![[Pasted image 20231110081944.png]]

## ALU design
### 1-bit version
![[Pasted image 20231110082912.png]]
### 8-bit version
![[Pasted image 20231110083204.png]]

## Data path timing
![[Pasted image 20231110083315.png]]
![[Pasted image 20231110083329.png]]

## Memory operation
On the Mic-1, we have two ways to access memory.
• Via MAR (Memory Address Reg.) / MDR (Memory Data Reg.) 32-bit reg. which accesses the  memory in word sizes (32-bit) 1 Giga addresses of 32-bit data (= 4GB)
• Via PC (Program Counter) / MBR (Memory Byte Reg.) 32-bit reg. which accesses the memory in byte sizes (8-bit) 4 Giga addresses of 8-bit data (= 4GB)
![[Pasted image 20231110083730.png]]
The MAR works by multiplying every memory address by 4, so the memory is read in words, but accessed by byte number.

### MBR (Memory Byte Register)
8-bit MBR can be put onto the 32-bit B bus in 2 different ways.

• Unsigned
Here the MBR is put on the 8 LSBs, the upper 24 bits are set to 0
![[Pasted image 20231110084717.png]]
• Signed
Here the MBR is put on the 8 LSBs, the upper 24 bits are set,
cf. the MSB bit in MBR (called Sign Extension)
![[Pasted image 20231110084740.png]]

## Memory Access Timing
![[Pasted image 20231110084818.png]]

## Micro Instructions Register (MIR)
In order to control the data flow and ALU functions in the Data Path, the Mic-1 uses
a special internal memory called Control Store for holding microinstructions.
The microinstructions from the Control Store is loaded into MIR, thereby
determining what should happen in the Data Path in the current Clock Cycle
![[Pasted image 20231110085138.png]]
![[Pasted image 20231110085423.png]]

### Branching Functionality
This functionality is determined by the JAM field in the microinstruction
High bit = (JAMZ AND Z) OR (JAMN AND N)
If JMPC = 1, then the address field is usually 0. The next instruction is determined
by the contents of the MBR register. In a typical use, MBR contains an opcode, so
the use of JMPC will result in a unique selection for the first microinstruction to be
executed for every possible opcode.
The first microinstruction in an instruction is located in the Control Store at the
address indicated by the machine code of the instruction.
![[Pasted image 20231110085856.png]]

### Local variables
Mic-1 uses stacks to support local variables (like all other machines)
Here, two registers are used as pointers that support this concept
• LV (Local Variable) points to the base of the local variables of the current procedure
• SP (Stack Pointer) points to the highest variable of the current procedure
![[Pasted image 20231110092304.png]]

### Operand stack
![[Pasted image 20231110092532.png]]

### IJVM Memory Model
![[Pasted image 20231110092652.png]]

## IVJM Instruction Set
![[Pasted image 20231110093507.png]]