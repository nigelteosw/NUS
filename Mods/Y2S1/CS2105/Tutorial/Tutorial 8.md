# Tutorial 8


## Question 1
In CSMA/CD, after the fifth collision, what is the probability that a node chooses 𝐾 = 4 ? The result 𝐾 = 4 corresponds to a delay of how many microseconds on a 10 Mbps Ethernet?

p(k = 4) = 1/32

After choosing K=4, node will wait for K * 512 bit times. Bit time for 10 Mbps ethernet is 0.1microsec. 
Therefore total waiting time for node = 4 * 512 * 0.1 microsec = 204.8 microsec

## Question 2

| Event | Switch table after event | Link(s) a frame is forwarded to |
| -----| ---------------------| ---------------------|
| B sends a frame to D | (B, 4) | 1,2 and 3 |
| D replies with a frame to B | (B,4) (D,3) | 4 |
| D sends a frame to A | (B,4) (D,3) | 1,2 and 4 |

## Question 3
a) Since A knows B’s MAC address from its ARP table, create a frame with B’s MAC addresses and send it to R which will forward it to host B. This frame travels to switch S and is forwarded towards B.

b) A will broadcast an ARP query packet, containing B's IP address. Switch will forward ARP query packet to  both B and R since estination MAC address is a broadcast address. R will ignore this query packet but B will reply to A. S will forward the reply frame towards A. Subseqyebtly A can send IP datagram to B.

c) A will broadcast an ARP query packet, containing B's IP address. only B will reply to A with its MAC address then the frame will be sent to A's MAC address. A will then send the data frame to B.

d) A creates IP datagram with IP source A, destination B. A will create a frame with R's MAC address as destination address, the frame will contain A-to-B IP datagram. Frame will be sent from A to R then passed up to IP. R forwards datagram with IP source A, destination B. R will create the frame with B's MAC address and forwards datagram with IP source A, destination B.


## Question 4
a) Source: IntelCor_2b:33:33 (84:5c:f3:2b:33:33)

b) Destination: HuaweiTe_4b:66:31 (e4:3e:c6:4b:66:31)

a)
