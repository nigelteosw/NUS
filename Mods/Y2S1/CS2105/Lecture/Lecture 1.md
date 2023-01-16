# Internet 

- The Internet is a network of connected computing devices
	- Also known as hosts or end systems
	- Host run network applications

## Network Edge ##
- Hosts access the internet through access networks
- Home Networks
	- Modem, router
- Enterprise Access Networks (Ethernet)
	- Typically in companies/universities
- Wireless Access Networks
	- Wireless LANs (aka Wi-Fi)
	- Wide-area wireless access (aka 3G/4G)
- Physical Media
	- Using cables

## Network Core ##
A mesh of interconnected routers.
Data is transmitted through:
1. Circuit switching: dedicated circuit per call
2. Packet switching: data sent through net in discrete chunks
   
### Circuit Switching ###
End-end resources allocated to and reserved for call between source and destination.
Call setup required
Reserving circuits for end to end connection

### Packet Switching ###
Hosts break application message into smaller chunks known as packets, length of L bits
- transmits packets to the link at transmission rate R
	- Link transmission rate aka link capacity or link badwith

packet transmision delay = time needed to transmit L-bit packet into link = L
(bits) / R (bits/sec)

- Store and forward: entire packet must arrive at a router before it can be transmitted on
- End-to-end delay = 2 * L/R
- Packets queue in router buffers (FIFO structure)
- Delays:
	- **processing delay:** packet being transmitted
	- **queueing delay:** packets queuing (queues have limited capacity resulting in buffer overflow)
	- d<sub>trans</sub> : **transmission delay**
		- L: packet length (bits)
		- R: link bandwith (bps)
		- d<sub>trans</sub> = L/R
	- d<sub>prop</sub>: **propogation delay**
		- d: length of physical link
		- s: propogation speed in medium 
		- d<sub>prop</sub> = d/s

**Throughput:** how many bits can be transmitted per unit time

**NOTE:**
Mbps vs MBps (bits vs bytes)

### Routing and Addressing ###
Routers determine source-destination using routing algorithms
- Addressing: each packet needs to contain source and destination information

Internet Structure: Network of Networks
- Host connects to Internet via access ISPs (Internet Service Providers)
- IP address and Internet Naming admistered by Network Information Centre (NIC)

### Network Protocols ###
Organized into "5 layers"
- Application
- Transport
- Network
- Link
- Physical
- (Presentation)
- (Session)