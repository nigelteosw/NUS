# MSI Components

## Decoders
- Convert binary information from n input lines to a maximum of 2<sup>n</sup> output lines
- Known as n-to-m-line decoder

### Implementing Functions
- A Boolean function, in *sum-of-minterms* form
	- decoder to generate the minterms
	- an OR gate to form the sum
- Good when circuit has many outputs and each function is expressed with a few minterms

Example: Implement the following function using a 3x8 decoder and an appropriate logic gate  
f(Q,X,P) = $\sum$ m(0,1,4,6,7) = $\prod$ M(2,3,5)

- We may implement the function in several ways:  
	- Using a decoder with active-high outputs with an OR gate: 
	  f(Q,X,P) = m0 + m1 + m4 + m6 + m7  
	- Using a decoder with active-low outputs with a NAND gate: 
	  f(Q,X,P) = (m0' $\cdot$ m1' $\cdot$ m4' $\cdot$ m6' $\cdot$ m7' )'  
	- Using a decoder with active-high outputs with a NOR gate: 
	  f(Q,X,P) = (m2 + m3 + m5 )' = M2 $\cdot$ M3 $\cdot$ M5  
	- Using a decoder with active-low outputs with an AND gate: 
	  f(Q,X,P) = m2' $\cdot$ m3' $\cdot$ m5'

### Decoders with Enable
- Decodes often come with an enable control signal, so that the device is only activated with the enable E=1
- Most MSI decodes, the enable signal is *zero-enable* usually denoted by E', decoder is enable when the signal is zero

### Constructing Larger Decoders
- Larger decodes can be constructed from smaller ones
- Decoders may have *zero-enable* and/or *negated outputs*
	- Normal outputs = active high outputs
	- Negated outputs = active low outputs


## Encoders
- Encoding is the converse of decoding
- Contains 2<sup>n</sup> input lines and n output lines
	- Implemented with OR gates
- To allow for more than one input line to carry a 1, we need priority encoder

### Priority Encoders
- A *priority encoder* is one with priority
	- If two or more inputs equal to 1, the input with the highest priority takes precedence
	- If all inputs are 0, this input combination is considered invalid


## Demultiplexers
- Helps share a single communication line among a number of devices
- At only one time, only one source and one destination can use the communication line

- Given an input line and a set of selection lines, a *demultiplexer* directs data from input to one selected data line
![[Pasted image 20221016195840.png]]


- Demultiplexer circuit is actually *identical* to a decode with enable

### Multiplexer
- A multiplexer is a device that has
	- A number of input lines
	- A number of selection lines
	- One output line
- It steers one of 2<sup>n</sup> inputs to a single output line, using n selection lines AKA *data selector*

![[Pasted image 20221016200535.png]]

### Implementing Functions
- Boolean functions can be implemented using multiplexers.
- A 2n-to-1 multiplexer can implement a Boolean function of n input variables, as follows:
	1. Express in sum-of-minterms form.
	   F(A,B,C) = A'$\cdot$B'$\cdot$C + A'$\cdot$B$\cdot$C + A$\cdot$B'$\cdot$C + A$\cdot$B$\cdot$C'  
	   = S m(1,3,5,6)