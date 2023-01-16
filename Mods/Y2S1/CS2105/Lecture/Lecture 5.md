# Transport Layer Part 2

## [[UDP]]

## Performance of rdt 3.0
- rdt 3.0 works, but performance stinks

$throughput = \frac {L} {RTT + dtrans}$

- Sender utilization is the fraction of time sender is busy sending
$sender = \frac {dtrans} {RTT + dtrans}$

## Pipelining
- Sender allows multiple, "in-flight" yet to be acknowledged packets
	- range of sequence numbers must be increased
	- buffering at sender or receiver

Two generic forms of pipeline protocols
- *Go-Back_N (GBN)*
- *Selective repeat (SR)*

### Go-Back-N
- Send 0,1,2,3
- If packet 2 is lost, discard and resend ACK1
- discard the rest of the packets
- when packet 2 timeout, resend from packet 2,3,4,5

**GBN Sender** 
- can have up to N unACKed packets in pipeline. 
- insert k-bits sequence number in packet header. 
- use a “sliding window” to keep track of unACKed packets. 
- keep a timer for the oldest unACKed packet. 
- `timeout(n)`: retransmit packet n and all subsequent packets in the window. 

**GBN Receiver** 
- only ACK packets that arrive in order. 
	- simple receiver: need only remember expectedSeqNum 
- discard out-of-order packets and ACK the last in-order seq. #. 
	- *Cumulative ACK*: “ACK m” means all packets up to m are received

### Selective Repeat
Receiver *individually acknowledges* all correctly received packets. 
- Buffers out-of-order packets, as needed, for eventual in-order delivery to upper layer. 

Sender maintains timer for *each* unACKed packet. 
- When timer expires, retransmit only that unACKed packet.

## TCP: 

- Point-to-point:
	- One sender, one receiver

- Connection-oriented:
	- handshaking (exchange of control messages) before sending app data

- Full duplex service:
	- bi-directional data flow in the same connections

- Reliable, in-order byte stream:
	- uses sequence  umbers to label bytes

### Connection-oreinted De-mux
- A TCP connection (socket) is identified by 4-tuple:
	- (srcIPaddr, srcPort, destIPAddr, destPort)

SYN packets are **normally generated when a client attempts to start a TCP connection to a server, and the client and server exchange a series of messages**

### TCP: Buffers and Segments
- TCP send and recieve buffers
- How much app-layer data can a TCP segment carry
	- maximum segment size (MSS), typically 1460 bytes (+ 20bytes)
	- app passes data to TCP then TCP forms packets in view of MSS

![[Pasted image 20220907121404.png]]

### TCP Sequence Number
- "Byte number" of the first byte of data in a segment

### TCP ACK Number
- Sequence number of the *next* byte of data exxpected by receiver
- TCP ACKs up the the first missing byte in the stream (cumulative ACK)
	- Note: TCP spec doesn't say how recceiver should handle out-of-order segments - it's up to implementer
- Initial sequence number is randomly chosen for the scope of this module

### TCP ACK Generation


### TCP Timeout Value
- *too short timeout*: premature timeout and unnecessary retransmissions.
- *too long timeout*: slow reaction to segment loss.
- Timeout interval must be slightly longer than RTT but RTT varies
- TCP computes (and keeps updating) timeout interval based on estimated RTT

EstimatedRTT = (1 - $\alpha$) * ExtimatedRTT + $\alpha$ * SampleRTT

DevRTT = (1-β) * DevRTT + β * |SampleRTT-EstimatedRTT|

TimeoutInterval = EstimatedRTT + (4 * DevRTT) 
where (4 * DevRTT) is the safety margin

### TCP Fast Retransmission
**Timeout period is often relatively long.** 
- long delay before resending lost packet

**Fast retransmission:** 
- Event: If sender receives 4 ACKs for the same segment, it supposes that segment is lost. 
- Action: resend segment (even before timer expires).