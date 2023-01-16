# Network Layer

## Network Layer Services
- Network layer delivers packets to receiving hosts.
	- Routers examine header fileds of IP datagrams


## IP Address
- IP address is used to identify a host (device or router)
	- A 32-bit integer expressed in either binary or decimal
- Binary to decimal going by part by part *(4 parts)*
	- 8 bit * 4
- Host get IP address?
	- manually by system administrator
	- automatically assigned by a *DHCP (Dynamic Host Configuration Protocol)* server

## Dynamic Host Configuration Protocol
- DHCP allows a host to dynamically obtain its IP address from the server when it joins network
	- reusable
	- support mobile users who want to join network

**4 Steps:**
1. Host broadcast "DHCP discover" message
2. Server responds with "DHCP offer" message
3. Host request IP address "DHCP request" message
4. DHCP server sends address "DHCP ACK" message

In addition to host IP address assignment, DHCP may also provide a host additional network info
- IP address of first-hop router
- IP address of local DNS server
- Network mask

*DHCP runs over UDP*
- DHCP server port number: 67
- DHCP client port number: 68

## Special IP Addresses
- 0.0.0.0/8 : non-routable meta-address for special use
- 127.0.0.0/8 : loopback address (local host) only when starting with the same first 8 bits which are 127
- 10.0.0.0/8 : private addresses
- 172.16.0.0/12 : private addresses 
- 192.168.0.0/16 : private addresses
- 255.255.255.255/32 : broadcast address. all hosts on the same subnet

## IP address and Network Interface
- An IP address is associated with a network interface.
	- A host usually has one or two network interfaces
	- A router typically multiple interfaces
- A network consisting of 3 subnets (first 24 bits of IP address are network prefix)

## Subnet 
- An IP address consists of two parts
	- n bits *subnet prefix*
	- 32 - n bits *host ID*
- **Subnet** is a network formed by a group of "directly" interconnected hosts
	- Hosts in the same subnet have the same network prefix
	- Hosts within the same subnet can physically reach each other without intervening router (first hop router)
	- Connect to outside world using a router


## IP Address: CIDR
- Classless Inter-domain Routing (CIDR)
	- The internet's IP address assingment strategy
	- Subnet prefix of IP address is of arbitary length
	- Address format: a.b.c.d/x where x is the number of bits in the subnet prefix


## Subnet Mask
- Used to determine which subnet and IP address belongs to
	- made by setting all subnet prefix bits to "1" and host ID bits to "0"s
	- can be used to infer how many bits are used for subnet prefix

## IP Address Allocation
- IP addresses can be bought from registry or rented from ISP's address space


## Heirarchical Addressing
- Second ISP will accept both the new and old IP addresses
- Use a forwarding table
- Use logest prefix match to find 

## More on IP Address Allocation
- ICANN: Internet Corporation for Assigned Names and Numbers
	- Allocates addresses
	- Manages DNS
	- Assigns domain names, resolves disputes