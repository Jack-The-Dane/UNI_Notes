## How the pipeline works in Mic-3
The shaded area indicate that the area is in use. When the pipeline is full, all areas are in use, but with different micro-instructions (e.g., cycle4) as we can see, there is no stalling in this sequence.
![[Pasted image 20231201085539.png]]

## How the pipeline works, general theory
In general, an instruction can divided into the following phases
• F – fetch. The instruction is retrieved into the CPU.
• D – decode. The instruction is decoded. (possible operands are retrieved)
• E – execute. The instruction is executed.
• W – write back. The result of the performed instruction is written back to the memory.
Micro-Instruction execution on CPUs without pipeline:
![[Pasted image 20231201085751.png]]
If 4 micro-instructions are executed in this way, it will take 16 ΔT , where each
clock cycle takes ΔT .

Same Instruction execution time as before, but better throughput as a new instruction is started every cycle
![[Pasted image 20231201085913.png]]
Just like before, the different areas of the data path are called Stages,
which take care of different tasks. See e.g., ΔT4:
• Stage 1 performs the F phase for instruction d
• Stage 2 performs the D phase of instruction c
• Stage 3 performs the E phase of instruction b
• Stage 4 performs the W phase for instruction a
Now, the same 4 instructions can be completed within 7 ΔT

## Pipeline hazards
We distinguish between 3 types of pipeline hazards:
• **Structural hazards**. These occur when there are resource conflicts, i.e.,
when the hardware cannot support certain combinations of instructions
simultaneously. If different instructions in different stages of the pipeline
are to use the same resource, we will get a pipeline stall.
• **Data hazards** occurs when an instruction depends on the result of a
previous instruction so that this result does not exist at the time when
it is to be used due to the instruction overlap.
• **Control hazards** occurs when branch jumps, or other flow control
commands change the instruction flow in program execution and
thus in the pipeline.
### Structural hazards
![[Pasted image 20231201091841.png]]
**Solution**
By duplicating resources, the problem can be remedied.
• Dual-cache (separate for opcode and data) with separate internal buses
• Multi-port CPU registers (e.g., MAR) and duplication of internal buses.

### Data hazard
Data hazards
We have previously mentioned Read After Write (RAW) hazard. Here's
an example:
![[Pasted image 20231201092104.png]]
#### Pipeline stall
![[Pasted image 20231201092214.png]]
By making a pipeline stall for 2 ΔT, the problem can be solved.
• Result from add instruction is known in ΔT4
• The result is used first in ΔT5 by sub instruction.
But a pipeline stall lowers down the throughput and performance

#### Out-of-order execution
![[Pasted image 20231201092252.png]]
Here 2 instructions (c and d), which have nothing to do with instructions
a and b, are inserted in between them, which fill the “hole” left by the pipeline stall.
This keeps the pipeline utilized completely and the optimal throughput
and performance can remain unchanged.
This reordering of tasks is handled by the assembler at compile time. It is not handles by the CPU itself or the programmer.

#### Forwarding
Forwarding is a design change of the Data Path.
Here, data hazards can be remedied in the case of register-to-register instructions.
If the instruction involves an access to the memory, then this solution is not applicable.
![[Pasted image 20231201092508.png]]

### Control hazards
This occurs when a branch needs to be made for a new target instruction
• A pipeline flush is performed in which all retrieved instructions in the pipeline are
deleted.
• Instructions from the new location are retrieved
• Consequence: performance deteriorates
Solution → Branch prediction
• The CPU is trying to guess the result of a branch.
• A branch that points backwards is taken approx. 90% of cases.
• A branch that points forward is taken approx. 50% of cases.
• Dynamic Branch prediction (recording and statistics) correct rate: approx. 90%
Solution → Branch target cache
• The first few instructions of each possible branch (corresponding to the size of
the pipeline) are stored in a special cache.
• The pipeline can then be overwritten from this cache, which is faster than
fetching instructions from memory again.
