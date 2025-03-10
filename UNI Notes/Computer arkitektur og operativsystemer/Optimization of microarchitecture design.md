## Design goals
There are many criteria to consider when designing microarchitecture, e.g.,:
• Speed
• Cost
• Ease of use
• Energy consumption
• Physical size
However, there is one trade-off that drives the most important decisions
around microprocessor design:
**Speed vs. Cost**
We will take a closer look at this trade-off

**The price depends primarily on the chip size**
• more complicated → bigger chip → more expensive
• less complicated → smaller chip →cheaper
**Optimization of the microcode (microinstruction)**
• Optimal microcode →Reduced number of cycles per IJVM →faster speed
**Modification of the data path**
• More flexible bus design →more microinstruction options
• more microinstruction options →Reduced number of cycles per IJVM
**Other hardware changes**
• Prefetching→Reduced number of cycles per IJVM →faster speed
• Pipelining→faster clock speed →faster speed
We will look at the different solutions

### Merging the main loop with the microcode: Example - POP
![[Pasted image 20231201082533.png]]

### Modification of the Data Path
![[Pasted image 20231201082617.png]]
### Instruction Fetch Unit
![[Pasted image 20231201083156.png]]
![[Pasted image 20231201083222.png]]

## Example: Mic-2
![[Pasted image 20231201083942.png]]
![[Pasted image 20231201084057.png]]
See slides for more microcode examples

## Example: Mic-3
![[Pasted image 20231201084134.png]]
This is called pipelined design.
### Difference between Mic-2 and Mic-3
![[Pasted image 20231201084723.png]]
![[Pasted image 20231201084733.png]]
