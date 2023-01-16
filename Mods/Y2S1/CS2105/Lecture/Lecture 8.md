# Lecture 8

## Link Layer

*Link layer* sends datagram between adjacent nodes (hosts or routers) over a single link.
- IP datagrams are encapsulated in link-layer frames for transmission
- Different link-layer protocols may be used on different links
- *data-link layer* has responsibility of transferring datagram from one node to *physically adjacent* node over a link

1. Each link needs to be addressed
2. Need to define a protocol
3. Need to handle errors

### Framing
Encapsulate datagram into frame, adding header and trailer

### Link access control
Need to coordinate which nodes can send frames at a certain point in time when a single link is shared

### Error detection
Errors are usually caused by signal attenuation or noise
Receiver detects presence of errors
- May signal sender for retransmission or just drop frames

### Error correction
Receiver identifies and corrects bit error(s) without resorting to retransmission

### Reliable delivery
Seldom used on low bit-error link but often use for error-prone links

### Link Layer Implementation
- Implemented in "adapter" or on a chip
	- E.g. Ethernet card, Wi-Fi adapter
- Adapters are semi-autonomous, implementing bot link & physical layers


## Error Detection 
**EDC:** Error Detection and Correction bits
**D:** Data protected by error checking, may include header fields

- Error detection schemes are not 100% reliable!
	- may miss some errors but rarely
	- larger EDC fields yields better detection and even correction

## Popular error detection schemes:
- checksum (TCP/UDP/IP)
- Parity Checking
- CRC (commonly used in ink layer)


### Parity Checking: Single bit
Assume that information has to be sent D has d bits
- In an even parity scheme, the sender includes one additional bit, based on the value, it makes the number of 1 bits in the data even
- Good for detecting single/odd bit errors
- Cannot detect even numbers of bits switching
- Works exceptionally well (Mathematically)
	- In reality, errors are clustered in "bursts"
	- Probability of undetected errors in a frame can approach 50%


### Parity Checking 2-D
- the d bits in D are divided into i rows and j columns
- parity value is calculated for each row and each column
- i + j + 1 bits used for error detection
- Can detect any two-bit error in data
	- dont know where to correct bits when errors are formed in a box
- 15 bits require 9 bits, overhead of 37.5%


### Cyclic Redundancy Check
- We want to transfer a non-binary number D without error
- R: the r digit error detection code
	- Sender needs to computer R easily
	- Receiver can verify the integrity of D easily
- Using the mathematical properties of "division"
	- Use a special r digit number G, called the generator
![[Pasted image 20221012205347.png]]

- **D:** data bits viewed as a binary number
- **G:** generator of r + 1 bits, agreed by sender and receiver beforehand
- **R:** the r bit CRC
- Calculations are done in modulo 2
	- Does not need carries
	- Both addition and subtraction are identical to XOR

- Easy to implement on hardware
- Powerful error-detection coding that is widely used in practice (e.g. Ethernet, Wi-Fi)
	- Can detect all odd number of single bit errors
	- CRC of r bits can detect
		- all burst errors of less than r + 1 bits
		- all burst errors greater than r bits with probability (1-0.5<sup>r</sup>)

CRC is also known as *Polynomial Code*

## Multiple Access Links and Protocols

### Two Types of Network Links
- **Type 1:** point-to-point link
	- Sender and receiver connected by a dedicated link
- **Type 2:** broadcast link
	- Multiple nodes connected to a shared broadcast channel
	- When a node transmits a frame the channel broadcasts the frame and every other node receives a copy

### Multiple Access Protocols
- Collision when two or more devices send their messages at the same time
	- **Random Access**
		- No coordination, collisions are possible
		- "recover" from collisions
		- Used in Ethernet
	- **Taking turns**
		- Each node takes turns to transmit
		- E.g. Question answer sessions in seminars
		- Used in Bluetooth, FDDI and token ring
	- **Channel partioning**
		- divide channel into fixed smaller "pieces"
		- allocate piece to a node for exclusive use
		- E.g. US Presidential debates
		- Used in GSM, radio, satellite systems

### Ideal multiple access protocol
**Desired Properties:**
1. Collision Free
2. Efficient: when only one node wants to transmit, it uses the full bandwith
3. Fairness: all nodes get equal treatment R/M
4. Fully decentralized:
	- no special node to coordinate transmissions

### Channel Partioning Protocols

#### TDMA 
*(time division multiple access)*
- Access to channel in "rounds"
- Each node gets fixed length time slots in each round
- Frame (a time frame)
- A lot of idle time

- Collision Free: Yes
- Efficiency:
	- Inefficient
	- Unused slots go idle
	- Maximum throughput is R/N
- Fairness: Perfectly Fair
- Decentralized: Yes


#### EDMA
*(frequency division multiple access)*
- Channel spectrum is divided into frequency bands
- Each node is assigned a fixed frequency band
- Unused transmission time in frequency bands go idle
- 6 nodes, 1, 3, 4 have frames

- Collision Free: Yes
- Efficiency:
	- Inefficient
	- Unused slots go idle
	- Maximum throughput is R/N
- Fairness: Perfectly Fair
- Decentralized: Yes

### "Taking Turns" Protocols

#### Polling

- Collision Free: Yes
- Efficiency:
	- *Higher efficiency*
	- Overhead of polling
	- Unused slots go idle
	- Maximum throughput is R/N
- Fairness: Perfectly Fair
- Decentralized: No
	- Master node is a single point of failure

#### Token Passing

- Special frame, token is passed from one node to next, sequentially
- When node receives a token
	- hold onto the token only if some frames to transmit
		- it sends up to a maximum number of frames and then forwards the token to the next node
	- otherwise pass the token to the next node

- Collision Free: Yes
- Efficiency:
	- *Higher efficiency*
	- Overhead of polling
	- Unused slots go idle
	- Maximum throughput is R/N
- Fairness: Perfectly Fair
- Decentralized: Yes

- *Downside*
	- Token loss can be disruptice
		- data frame loss
		- system bugs
	- Node failure can break the ring


### Random Access Protocols

- When a node has data
	- Transmit at full channel data rate R
	- no a priori coordination among nodes
- Two or more transmitting nodes -> " collision"

- Random access protocols specify
	- how to detect collisions
	- how to recover from collisions

- Slotted ALOHA, ALOHA
- CSMA, CSMA/CD


- One major *design flaw* in ALOHA
	- a node's decision to transmit is made independently of the activity of the other nodes
	- a node *pays no attention* to whether a node happens to be transmitting when it begins to transmit

- One major *design flaw* in ALOHA and CSMA
	- a node *does not stop* transmitting even when collision is detected


#### Slotted aloha

**Design:**
- All frames are of equal size, L bits
- Time is divided into slots of equal length
	- length = time to transmit 1 frame = L/R
- Nodes start to transmit only at the begining of a slot

**Operation:**
- Node has a fresh frame to send
	- wait until the begining of next slot and transmits the entire frame in the slot
	- no collision: data transmission success
	- collision: retransmit the frame in each subsequent slot with probabily p until success

- Collision Free: No
- Efficiency:
	- Yes, when only 1 node is active
	- No, when many nodes, maximum efficiency is only 37%
		- slots are wasted due to collision and being empty
		- 100 Mbps system will only give 37 Mbps
- Fairness: Perfectly Fair
- Decentralized: Yes


#### Pure (unslotted) ALOHA

- No time slots
- No Synchronization
- Chance of collision increases

**Operation:**
- When node has a fresh frame to send
	- Transmits the frame immediately
	- no collision: data transmission success
	- collision: retransmit the frame in 1 frame transmission time with probabily p until success

- Collision Free: No
- Efficiency:
	- Yes, when only 1 node is active
	- No, when many nodes, maximum efficiency is only 18%
		- slots are wasted due to collision and being empty
		- 100 Mbps system will only give 18 Mbps
- Fairness: Perfectly Fair
- Decentralized: Yes


#### CSMA
- Carrier Sense Multiple Access
- if channel *sensed idle*: transmit entire frame
- if channel *sensed busy*: defer transmission

- Collision Free: No
	- *propogation delay* means that two nodes may not hear each transmission immediately
- Efficiency:
	- Yes, when only 1 node is active
	- No, when many nodes, maximum efficiency is only 18%
		- slots are wasted due to collision and being empty
		- 100 Mbps system will only give 18 Mbps
- Fairness: Perfectly Fair
- Decentralized: Yes


#### CSMA/CD Backoff Algorithm
- if channel *sensed idle*: transmit entire frame
- if channel *sensed busy*: defer transmission
- if *collision detected*: abort transmission
	- retransmit after a random delay

- Major Drawback
	- The probability of collision in all subsequent time slots remain the same
	- It can even increase if a new node starts transmitting

- *Goal:* adapt retransmission attempts to estimated current load
	- more collisions implies heavier load
	- longer back-off interval with more colisions

**Binary Exponential backoff:**
- After first collision;
	- choose K at random from {0, 1};
	- wait K time units before retransmission
	- p = 1/2
- After second collision:
	- choose K from {0, 1, 2, 2<sup>2</sup>-1};
	- p = 1/4
- After m<sup>th</sup> collision:
	- choose K from {0, 1, 2, 2<sup>m</sup>-1};
	- p = 1/2<sup>m</sup>
- More collisions = longer back-off interval

**Minimum Frame Size**
- Collision happens but may not be detected by sending nodes
	- *No retransmission!*
- Ethernet requires a minimum frame size of 64 bytes

Collision Free: NO
	- *propogation delay* means that two nodes may not hear each transmission immediately
- Efficiency: Yes
- Fairness: Perfectly Fair
- Decentralized: Yes