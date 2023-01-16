# Transport Layer Part 1

## Transport Layer Services##
Deliver messages between application processes running on different hosts
1) **TCP**
2) **[[UDP]]**

Transport layer protocols run in hosts.
- **Sender side:** breaks app message into *segments* (as needed), passes them to network layer
- **Receiver side:** reassembles segments into message
- **Packet switches(routers) in between:** check destination IP address to decide routing

### [[UDP]]###
- UDP adds very little service on top of IP:
	- Multiplexing at sender: gather data from processes, forms packet then passes them to IP
	- De-multiplexing at receiver: receives packets from lower layer and dispatches them to the right processes
	- Checksum
- When UDP recceiver receves a UDP segment:
	- Checks destination port # in segment
	- Directs UDP segment to the soceket with the port #.
	- IP datagrams with the same destination port # will be directed to the same UDP socket at destination.
- 1-to-many system 
- UDP Checksum
	- to detect "errors" in the transmitted segment.
	- Sender: compute checksum value, puts value into UDP checksum field
	- Receiver: compute checksum and confirms if both are equal
	- *It will detect any single bit flip, but if the packet is altered such that the sum of all the data as 16 bit values remains constant, the checksum will not detect the error.*

### Checksum Computation###
1) Treat UDP segment as a sequence of 16-bit integers
2) Apply binary addition on every 16-bit integer
3) Carry (if any) from the most significant bit will be added to the result
4) Compute 1's complement to get UDP checksum

**NOTE: do a wraparound carry**

- Transport layer residdes on end hosts and provides **process-to-process** communication
- Network layer provies **host-to-host, best-effort** and **unreliable** communication

Underlying network may:
- corrupt packets
- drop packets
- re-order packets (not considered)
- deliver packets after such a long delay

End-to-end reliable transport service should
- gurantee packet delivery and correctness

## [[UDP]]

### rdt 2.0: Channel with Bit Errors###
Assume that underlying channel may flip bits in packets
Stop and wait protocol

1) How to detect bit errors?
	1) Using a checksum to detect bit errors
2) How to recover from bit errors?
	1) Acknowledgements: receiver explicitly tells sender that packet recieved is ok
	2) Negative acknowledgements: reciever tells sender that packet has errors

What happens when ACK/NAK is corrupted?
May cause retransmission of recieved packet

### rdt 2.1: rdt 2.0 + Packet Sequence Number###
To handle duplicates
- sequence number is sent with each packets
- receiver discards duplicate packet

### rdt 2.2: a NAK-free Protocol###
- Same as rdt 2.1, but uses ACK only
- instead of sending NAK, receiver sends ACK for the last packet recieved OK
	- receiver must explicitly include sequnece number of the packet being acked
- Duplicate ACKs results in the same action as NAK

### rdt 3.0: Channel with Errors and Loss###
- Assumption: underlying channel
	- may flip bits in packets
	- may lose packets
	- may incur long packet delays
	- but will not reorder packets

Question: How to detect packet loss
- To handle packet loss, sender waits "reasonable" amount of time for ACK until timeout
- Timeout will trigger retransmission

## RDT Summary##
| rdt Version | Scenario | Features Used |
| --------- | -------- | ------------| 
| 1.0 | no error | nothing |
| 2.0 | data Bit Error | checksum, ACK/NAK | checksum, ACK/NAK |
| 2.1 | Data Bit Error, ACK/NAK Bit Error | sequence Number |
| 2.2 | Same as 2.1 | NAK free |
| 3.0 | Same as 2.1 but with packet loss | timeout/re-transmission |


