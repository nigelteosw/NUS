# Tutorial 1
1)   [KR, Chapter 1, P6]
	a) d<sub>prop</sub> = m/s sec where m is the distance between the two hosts and s is the speed of the link.
	b) d<sub>trans</sub> = L/R sec
	c) d<sub>end-to-end</sub> = d<sub>prop</sub> + d<sub>trans</sub> = m/s + L/R sec
	d) just left Host A / just arrive on the link
	e) somewhere along the link but not at Host B
	f) it has already arrived at the destination Host B
	g) m/s = L/R, m = Ls/R = 120b * 2.5 * 10<sup>8</sup> / 56 * 10<sup>3</sup> = 535714.2857m
	round off to 5s.f. 

2) A packet switch receives a packet and determines the outbound link to which the packet should be forwarded. When the packet arrives, one other packet is halfway done being transmitted on this outbound link and four other packets are waiting to be transmitted. Packets are transmitted in order of arrival. Suppose all packets are 1,500 bytes and the link rate is 2 Mbps.
   
	a) Packet transmission delay = 
	Bytes of packets remaining = (0.5 + 4) * 1500 = 6750 bytes or 54000 bits
	Since the packets are transmitted at 2Mbps
	Queuing delay = 54000 / (2 * 10<sup>6</sup>) = 27msec (length of packet remaining/rate)
	
	b) Remainding bits = L - x
	number of bits = Nx
	/ R

3) [Modified from KR, Chapter 1, P31]

	a) (8 * 10<sup>6</sup>) / (2 * 10<sup>6</sup>) = 4s
	
	b) 4s * 3 = 12s (3 hops)
	
	c) First packet from src to first switch: 0.005s
	    Second packet to the first switch: 0.01s
	    
	d) 4.01s 
	
	e) In the case when there is an error with the entire package, for message segmentation, the entire message does not need to be transmitted again, thus saving time/data. 
	
	If huge packets are being sent into the network, routers have to accomodate the huge packets. Smaller packets have to queue behind these huge packets and suffer unfair delays.
	
	f) If one segmented packet is missing, then the overall file cannot be read.
	
	Time needed to restore the package together (network may re-order packets).
	
	Each small packets need to carry the packet header in size tens of bytes (e.g. to the specific destination address and port number). This is the header overhea of each packet to be discussed in later lectures.

	**NOTE:**
	message segmentation may not be faster, but is good when there are many many routers. Because of the headers, the packets itself have a bigger size.

4) There are N devices to be connected. There can be either 0 or 1 link between any 2 devices.

	a) N-1 (tree, chain, star network topology)
	
	b) N(N-1)/2  (all devices connected to all other devices directly. Mesh network topology)
	
	c) A requires less links hence the cost and complexity of A will be reduced compared to B. 
	
	However B is more robust as the breakdown of a device does not affect other devices in the network. (more tolerable to link failure) More wires and configurations needed, more expensive to deploy.