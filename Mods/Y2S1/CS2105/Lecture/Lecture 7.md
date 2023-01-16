# Network Layer

## Routing Algorithms

### Internet: Network of Networks
- Done in a heirarchichal way 

### Autonomous System
**Intra-AS** routing
- Finds a good path between two routers within an AS
- Protocols: RIP, OSPF

**Inter-AS** routing
- Handles the interfaces between AS.
- Protocols: BGP

## Intra-AS Routing
- We associate a cost to each link
	- Cost could always be 1 or inversely related to bandwith, or related to congestion
- Routing: finding a least cost path between two vertices in a graph

*"link state" algorithms*
- All routers have complete knowledge of the network topology and link cost
	- Routers periodically braodcast link cost to each other
- Use Dijkstras Algorithm

*"distance vector" algorithms*
- Routers know physically-connected neighbours and link cost
- Routers exchange "local views" with **direct neighbours**
- Iterative process of computation
	- Swap local view with direct neighbours


`c(x,y)` : the cost of link between routers X and Y

`dx(y)` : the cost of the least-cost path from x to y (from x's view)

## Bellman-Ford Equation
![[Pasted image 20221012124303.png]]
Where min is taken over all direct neighbours v of x

To find the least cost path, x needs to know the cost from each of its direct neighbour to y
- Each neighbour v sends its distance vector to x telling x that the cost of v to y is k


## RIP (Routing Information Protocol)

- Implements the DV algorithm. It uses hop count as the cost metric (insensitive to network congestion)
- Exchange routing table every 30s over UDP port 520
- Self repair: if no update from neighbour router for 3 mins, assume neighbour has failed


## NAT (Network Address Translation)

NAT routers must:
- Replace (source IP address, port #) of every outgoing datagram to (NAT IP address, new port #).
- Remember (in NAT translation table) the mapping from (source IP address, port #) to (NAT IP address, new port #).
- Replace (NAT IP address, new port #) in destination fields of every incoming datagram with corresponding (source IP address, port #) stored in NAT translation table

**Steps:**
1. host 172.26.184.3 sends datagram to 128.119.40.186, 80
2. NAT router changes datagram source addr, port, updates table
3. reply arrives. Dest address is: 137.132.228.5, 5001
4. NAT router changes datagram dest addr from 137.132.228.5, 5001 to 172.26.184.3, 3213

- No need to rent a range of public IP addresses from ISP: just one public IP for the NAT router. 
- All hosts use private IP addresses. Can change addresses of hosts in local network without notifying the outside world. 
- Can change ISP without changing addresses of hosts in local network. 
- Hosts inside local network are not explicitly addressable and visible by outside world (a security plus).


## IPv4 Datagram Format
![[Pasted image 20221012155054.png]]
- TTL will decrement by one through each hop (hop limit)

### IP Fragmentation & Reassembly
- Different links may have different *MTU (Max Transfer Unit)* – the maximum amount of data a link-level frame can carry.
- “Too large” IP datagrams may be fragmented by routers.
	- Big fragment broken down into multiple fragments
- Destination host will reassemble the packet.
- IP header fields are used to identify fragments and their relative order.

### IP Fragmentation
![[Pasted image 20221012155418.png]]
- Example
	- 20 bytes of IP header
	- 1200 byte IP datagram
	- MTU = 500 bytes

In this case, message will all be 480 bytes with 20 bytes as the IP header
480 + 480 + 220
ID remains unchanged

*Flag (frag flag)* is set to 
- 1 if there is next fragment from the same segment. 
- 0 if this is the last fragment

*Offset* is in expressed in unit of 8-bytes.


## IPv6
- IPv6 is designed to replace IPv4
- Primary motivation: 32-bit IPv4 address space is soon to be fully allocated
- IPv6 datagram:
	- 40 byte header (128 bits for source IP, 128 bits for destination IP)


## ICMP 
**Internet Control Message Protocol**
- used by hosts and routers s to communicate network-level information
- ICMP messages are carried in IP datagrams.
	- ICMP header starts after IP header.

- ICMP header: Type + Code + Checksum + others.
![[Pasted image 20221012160046.png]]

### ping and traceroute
- The command *ping* sees if a remote host will respond to us – do we have a connection?
- The command *traceroute* sends a series of small packets across a network, and attempts to display the route (or path) that the messages would take to get to a remote host.