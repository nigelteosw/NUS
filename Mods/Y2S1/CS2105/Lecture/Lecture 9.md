# The Link Layer, LAN


## Switched Local Area Networks

**Aim:** Send data between N nodes via cable

**Solution:** Inter-Connect the N nodes via a broadcast link
- each link needs to be *addressed*
- need to define a *protocol*
- need to handle *errors*


### MAC address
- Every adapter has a MAC address
	- Used to send and receieve link layer frames
	- When adapter recieves a frame that has the same MAC address, it extracts the datagram and passes it to the protocol stack

- MAC address is typically 48 bits burned in NIC (Network Interface Card) ROM (Read-only Memory)
	- MAC address allocation admistered by IEEE where the first 3 bytes identifies the vendor of an adapter
	- Broadcast Address: FF-FF-FF-FF-FF-FF-FF

Data-link layer has responsibility of transferring datagram from one node to physically adjacent node over a link


## Local Area Network (LAN)
LAN is a computer network that interconnects computers within a *geographical area* such as office building or university campus.

LAN technologies: 
- IBM Token Ring: IEEE 802.5 standard 
- Ethernet: IEEE 802.3 standard 
- Wi-Fi: IEEE 802.11 standard 
- Others


## Ethernet
"Dominant" wired LAN technology
- Developed in mid 1970s, standardised by Xerox, DEC and Intel in 1978
- Simpler and cheaper than Token Ring and ATM


### 802.3 Ethernet Standards
- A series of Ethernet standards have been developed over the years
- Different speeds: 2 Mbps, 10 Mbps, 100 Mbps, etc
- Different physical layer media: cable, fiber optics
- MAC protocol and frame format remain unchanged


### Ethernet Frame Structure
- Consider the case of sending an ip datagram from one host to another on the same Ethernet Lan
- Sending NIC (adapter) encapsulates IP datagram in Ethernet frame
- Source and Dest MAC address:
	- If NIC recieves a frame with the matching destination address, or with broadcast address
	- passes the frame to network later protocol
	- else, NIC discards frame
- *MTU:* Maximum Transmission Unit

- **Data:** 
	- The maximum size is 1500 bytes. 
		- This maximum size is the link MTU which we mentioned when we discussed IP fragmentation. 
	- The minimum size is 46 bytes 
		- The minimum size is to ensure that a collision will always be detected.


- **CRC:** 4 bytes at the end
	- Corrupted frame will be dropped

- **Type:** Indicates higher layer protocol
	- Hosts can use other network-layer protocols other than IP
	- Type field permits Ethernet to multiplex network-layer protocols
	- Type field is analogus to
		- the protocol field in the network-layer datagram
		- the port-number fields in the transport-layer segment

- **Preamble:** 
	- 7 bytes with pattern 10101010 (AAhex)
	- Followed by 1 byte with pattern 10101011 (ABhex)
		- *"start of frame"*
	- used to synchronize receiever and sender clock rates
	- provides a "square wave" pattern that tells the receiver the sender's clock rate
		- width of a bit


### Ethernet Data Delivery Service
- Unreliable: receiving NIC doesn’t send ACK or NAK to sending NIC. 
	- data in dropped frames will be recovered only if initial sender uses higher layer rdt (e.g. TCP); otherwise dropped data is lost

- Ethernet’s multiple access protocol: 
	- CSMA/CD with binary (exponential) backoff. (handling collision)


### Ethernet: Physical Topology
Hub - cheap, slow
Switch - expensive fast


### Ethernet: Bus Topology
*Bus* topology: popular until mid 90s

The original Ethernet LAN used a coaxial bus to interconnect the nodes.

*Is a broadcast LAN* 
- All transmitted frames received by all adapters connected to the bus.
- all nodes can collide with each other 

*Drawbacks:* 
- Back bone cable 
	- If damaged, the entire network will fail 
	- Difficult to troubleshoot problems 
	- Very slow and not ideal for larger networks 
		- Due to collision


### Ethernet: Star Topology
*Star* topology: prevalent today

#### HUB
- Popular in late 1990’s 
- nodes are directly connected to a hub 
- A hub is a *physical-layer* device that acts on individual bits rather than frames. 
	- When a bit arrives from one interface, 
		- the hub simply re-creates the bit 
		- boosts its energy strength, and 
		- transmits the bit onto all the other interfaces.

**Advantages:**
- Cheap
- Easy maintainence
	- Modular design of the network

**Drawbacks:**
- Very slow and not ideal for larger networks
	- Due to collision

#### switch
- Popular since early 2000's
- nodes are directly connected to a switch
- A switch is a *layer-2* device
	- Works acts on frames rather than individual bits
	- *No collisions*
	- A bona-fid store and forward packet switch

### Ethernet Switch
A link-layer device used in LAN 
- Examine incoming frame’s MAC address 
- selectively forward frame to one-or-more outgoing links. 
- A switch does not have a MAC address

*Store and forward* Ethernet frames 
- uses *CSMA/CD* to access link

*Transparent* 
- hosts are unaware of presence of switches -
- Plug-and-play (self-learning) 
- switches do not need to be configured

Nodes have *dedicated, direct* connection to switch
- switches *buffer* packets


**Interconnecting Switches**
- Can be connected in heirachy
- Selective forwarding
	- Each switch has a switch table
	- Looks like a routing table


**Switch: Self-learning**
- Switch *learns* which hosts can be reached through which interfaces
- when frame is received, switch "learns" location of sender
- *records* sender/location pair in the switch table


**Switch: frame filtering/forwarding**
When frame received at switch: 
1. Record incoming link, MAC address of sending host 
2. Index switch table using MAC destination address 
3. if entry found for destination 
	1. if destination on segment from which frame arrived 1. drop frame 
	2. else forward frame on interface indicated by entry 
4. else flood 
	1. forward on all interfaces except arriving interface


## ARP 
**Address Resolution Protocol**

- Each IP node has an ARP table
	- Stores the mappings of IP address and MAC address of other nodes in the same subnet

Suppose A wants to send data to B in the same subnet
1. A knows B's MAC address
	1. Only create a frame with B's MAC address
	2. Only B will process this frame
2. A does not know B's MAC address
	1. Broadcasts an ARP query packet, containing B's IP address
	2. B replies to A with its MAC address
	3. A caches B's IP-to-MAC address mapping in its ARP table

ARP is *"plug-and-play"*
- Nodes create their own ARP tables without intervention from network administrator


Sending Frame to Another Subnet
- A creates a frame with a MAC address that is not in the library
- Instead of creating a frame with B's MAC address, send the frame to R which is the router
	- R will forward the datagram to another subnet



**IP Address vs. MAC Address**
| IP Address | MAC Address |
|----------|--------------|
| 32 bits in length | 48 bits in length |
| network-layer address used to move datagrams from source to dest | link-layer address used to move frames over every single link|
| Dynamically assigned; hierarchical (to facilitate routing) | Permanent, to identify the hardware (adapter) |
| Analogy: postal address | Analogy: NRIC number |
