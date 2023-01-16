# Tutorial 5

## Discussion Question

### D1
i. add $t0, $s0, $s1

a) 0x02114020
b) RegDst = 1, RegWrite = 1, Branch = 0
c) RR1: 16, Yes
    RR2: 17, Yes
d) Register: 8
    WriteReg = 1

ii. bne $24, $25, finish

a) 0x17190002
b) RegDst = 0, RegWrite = 0, Branch = 1
c) RR1: 24, Yes
    RR2: 25,
d) Register: 
    WriteReg = 0


## Tutorial Questions

### Question 1
a)

| RR1  | RR2  |  WR |  WD |  Opr1 | Opr2  | Address  | Write Data  |
|---|---|---|---|---|---|---|---|
| $15 | $24 | $24 | MEM([$15] + 0) | [$15] | 0 | [$15] + 0 | [$24] |
| $1 | $3 | $3 or $0 | [$1] - [$3] or some unknown value | [$1] | [$3] | [$1] - [$3] | [$3] |
| $20 | $5 | $25 | [$20] - [$5] | [$20] | [$5] | [$20] - [$5] | [$5] |


|RegDst|RegWr|ALUSrc|MRd|MWr|MToR|Brch|ALUop|ALUctrl|
|---|---|---|---|---|---|---|---|---|
|0|1|1|1|0|1|0|00|0010|
|X|0|0|0|0|X|1|01|0110|
|1|1|0|0|1|0|0|10|0110|

b)
	i. 0x8df80004
	ii. 0x10230040
	iii. 0x0285c826


### Question 2

a) 920ps + MUX
400 + 200 + 30 + 120  +30  + 200 = 980ps
b) 1170ps + MUX
400 + 200 + 120 +350 + 30 + 200 = 1300ps
c) 640ps
400 + 200 + 30 + 120 + 20 + 30 = 800ps

Cycle time should be 1170ps + MUX
PC is on the next rising edge of the clock

### Question 3

i. One example where the incorrect processor still gives the right execution result.

a) when both RT and RD are the same, e.g. `add $t1, $t0, $t1`
b) make the first 5 bits of the immediate value the same as the register number of RT
c) does not matter since WR is irrelevant

ii. One example where the incorrect processor gives the wrong execution result.

a) rt and rd are not the same
b) any other answer
c) no answer