# Pipelining Hazards


## Pipeline Hazards
Problems that prevent the next instruction from immediately following previous instruction

**Structural hazards**
Simultaneous use of a hardware resource

**Data hazards**
Data dependencies between instructions

**Control hazards**
Change in program flow


### Structural Hazard
More than one instruction uses the hardware at the same time

Solution 1: Stall the pipeline by as many cycles as needed

Solution 2: Split memory into data and instruction memory


### Data Dependency
When different instructions read/write to the same register
- register contention is the cause of dependency

**RAW**
- Read after Write dependency (true data dependency)
- Occurs when a later instruction reads from the destination register written by an earlier instruction
- Only the one that causes pipeline hazards

Solution:
- Forward the result to any trailing (later) instructions before it is reflected in the register file
- Bypass (replace) the data read from register file
- LOAD instruction cannot be solved before forwarding
	- Stall the pipeline

**WAR**
- Write after Read dependency 

**WAW**
- Write after Write dependency

### Control Dependency
When the execution of an instruction depends on another instruction
- control flow is the cause of dependency
- An instruction j is control dependent on i if i controls whether or not j executes

- If the registers involved in the comparison is produced by the preceding instruction, further stall is still needed


**Early Branch Resolution**
- Make decision in ID stage instead of MEM
	- Move register comparison -> cannot use ALU for register comparison any more
- If the registers involved in the comparison is produced by the preceding instruction, further stall is still needed

Solution: 
- Add forwarding path from ALU to ID stage
- One clock cycle delay is still needed

Problem is worse with load followed by branch

Solution:
- MEM to ID forwarding and 2 more stall cycles
- In this case, we ended up with 3 total stall cycles

**Branch Prediction**
All branches are assumed to be not taken

Correct Prediction: branch is not taken
- No stall required

Wrong prediction: branch is taken
- Flush the current instruction from the pipeline

**Delayed Branching**
- Branch outcome takes X number of cycles to be known
- Move non-control dependent instructions into the X slots following a a branch (do as to create a buffer)
	- These instructions are executed regardless of the outcome

**Best case scenario**
- Instructions preceding the branch can be moved into the delayed slot

**Worse case scenario**
- Add a no-op instruction in the branch-delay slot to delay the instruction