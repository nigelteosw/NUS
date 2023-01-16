# Sequential Logic

Two classes of logic circuits 
- Combinatorial 
- Sequential

## Sequential Circuit
- Depends on both input as well as state
- Two types:
	- Synchronous - outputs change only at specific time
	- Asynchronous - outputs change at any time
- Multivibrator: a class of sequential circuits
	- Bistable - 2 stable states
	- Monostable - 1 stable state
	- Astable - no stable state
- Bistable logic devices
	- Latches and flip-flops
	- differ in methods in changing their states

## Memory Elements
- A device that remembers values indefinitely and can change value on command from inputs
- Characteristic table to keep state
![[Pasted image 20221023224432.png | 400]]

Memory clock is usually a square wave
- Pulse-triggered
	- flat parts
	- Latches
	- ON = 1
	- Off = 0
- Edge-triggered (Program Counter)
	- vertical parts
	- Flip-flops
	- Positive edge-triggered (ON = from 0 to 1, OFF = other time)
	- Negative edge-triggered (ON = from 1 to 0, Off = other time)

## Latches

### S-R Latch
- Set and Reset
- Q = HIGH, latch is in SET state
- Q = LOW, latch is in RESET state
- For active-high input S-R latch (also known as NOR gate latch)
	- R = HIGH and S = LOW, Q becomes LOW (RESET state) 
	- S = HIGH and R = LOW, Q becomes HIGH (SET state)  
	- Both R and S are LOW, No change in output Q  
	- Both R and S are HIGH, Outputs Q and Q' are both LOW (invalid!)  

- Drawback: invalid condition exists and must be avoided.

![[Pasted image 20221023225431.png | 400]]


### Gated S-R Latch
- SR latch + enable input (EN) and 2 NAND gates
- basically swapping outputs when EN is high

![[Pasted image 20221023230400.png | 400]]


### Gated D latch
- Make input R equal to S' 
- D latch eliminates the undesirable condition of invalid state in the S-R latch
- Will memorize the state when EN = 0
- When EN is high, Q "follows" the D input
	- D = High -> latch is set
	- D = Low -> latch is reset


![[Pasted image 20221023230746.png | 400]]
![[Pasted image 20221023231052.png | 400]]


## Flip-flops
- Flip-flops are synchronous bistable devices
- Output changes state at a specified point on a triggering input called the clock
- Change state at the edges


### S-R flip-flop
- R flip-flop: On the triggering edge of the clock pulse,  
- R = HIGH and S = LOW  Q becomes LOW (RESET state)  
- S = HIGH and R = LOW  Q becomes HIGH (SET state)  
- Both R and S are LOW No change in output Q  
- Both R and S are HIGH Invalid!

Now it is dependent on the rising edge of the clock

![[Pasted image 20221023231526.png  | 400]]


### D Flip-flop
- D flip-flop, single input D dependent on the triggering edge of the clock's pulse
	- D = HIGH  Q becomes HIGH (SET state)  
	- D = LOW  Q becomes LOW (RESET state)

**Application**
- Parallel data transfer
	- To transfer logic-circuit outputs X, Y, Z to flip-flops Q1, Q2 and Q3 for storage


### J-K Flip-Flop
**J-K flip-flop:** Q and Q' are fed back to the pulse-steering NAND gates
- No invalid state
- Include a toggle state:
	- HIGH and K = LOW - Q becomes HIGH (SET state)  
	- K = HIGH and J = LOW - Q becomes LOW (RESET state) 
	- Both J and K are LOW - No change in output Q  
	- Both J and K are HIGH - Toggle

![[Pasted image 20221023232030.png | 400]]


### T Flip-flop
**T flip-flop:** Single input version of the J-K flip-flop, formed by tying both inputs together.

![[Pasted image 20221023232208.png | 400]]


## Asynchronous Inputs
- S-R, D and J-K inputs are synchronous inputs, as data on these inputs are transferred to the flip-flop's output only on the triggered edge of the clock pulse
- synchronous inputs affect the state of the flip-flop independent of the clock; example: preset (PRE) and clear (CLR) (or direct set (SD) and direct reset (RD)).


## Sequential Circuits Analysis
- From *state equations* and *output function*, we can derive the *state table*, consisting of the binary combinations of all present states and inputs
- m flip-flops and n inputs result in 2<sup>m+n</sup> rows
- *State table* for circuit of Figure 1:

### State Diagram
- each state is denoted by a circle
- each arrow denotes a transition of the sequential circuit
- each combination of the flip-flop values represent a state
	- m flip-flops => up to 2<sup>m</sup> values

- Circuits are determined by circuit output functions


## Excitation Tables
**Excitation tables:** given the required transition from present state to next state, determine the flip-flop inputs


## Memory
- Memory stores programs and data
- Definitions:  
	- 1 byte = 8 bits  
	- 1 word: in multiple of bytes, a unit of transfer between main memory and registers, usually size of register.  
	- 1 KB (kilo-bytes) = 210 bytes; 1 MB (mega-bytes) = 220 bytes;  
	- 1 GB (giga-bytes) = 230 bytes; 1 TB (tera-bytes) = 240 bytes.
- Desirable properties: fast access, large capacity, economical cost, non-volatile.

Memory is divided into pigeonholes and each has an address.
- Memory Address Register (MAR) that generates the address
- Memory Data Register (MDR)


The data consists of n lines (for n-bit words). Data input lines provide the information to be stored (written) into the memory, while data output lines carry the information out (read) from the memory.

The address consists of k lines which specify which word (among the 2k words available) to be selected for reading or writing.

The control lines Read and Write (usually combined into a single control line Read/Write) specifies the direction of transfer of the data.

- **Write** operation:
	- Transfers address of the desired word into the address lines
	- Transfers the data bits (the word) to be stored in memory to the data input lines
	- Activates the Write control line (set Read/Write to 0)

- **Read** operation:
	- Transfers the address of the desired word to the address lines
	- Activates the Read control line (set Read/Write to 1)


### Memory Cell
- Two types of RAM
	- Static RAMs use flip-flops as the memory cells
	- Dynamic RAMs use capacitor charges to represent data. Though simpler in circuitry, they have to be constantly refreshed
- A simple memory cell of the static RAM has the following logic and block diagrams
	- Basically a D flip-flop
	- ![[Pasted image 20221024013841.png | 400]]


