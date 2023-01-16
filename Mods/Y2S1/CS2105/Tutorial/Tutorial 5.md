# Tutorial 5 

## Question 1
Binary equivalent of 202.3.14.25: 11001010 00000011 00001110 00011001


## Question 2
40 bytes data, 20 bytes TCP header, 20 bytes IP header
percentage of overhead: 50%
percentage of application data: 50%
why we should not segment it too much as it is every inefficient
message segmentation only works when there are *multiple hops*


## Question 3
000010000 00011011 00011000 ~~00000000~~
The block IP address will be: 16.27.24.0/24


## Question 4
a) 192.168.52.130
b) Suppose an ISP owns the block of addresses of the form 192.168.56.128/26
| Network Prefix | Binary Expression |
|-----------------|--------------------|
| 192.168.59.128/28 | 11000000 10101000 00111010 10**00**0000 |
| 192.168.59.144/28 | 11000000 10101000 00111010 10**01**0000 |
| 192.168.59.160/28 | 11000000 10101000 00111010 10**10**0000 |
| 192.168.59.176/28 | 11000000 10101000 00111010 10**11**0000 |


## Question 5
| First IP | Last IP | Number of IP addresses |
|--------|---------|---------------------------|
| 11000000 | 11111111 | 64 |
| 10100000 | 10111111 | 32 |
| 10000000 | 10011111 | 32 |
| 00000000 | 01111111 | 128 |


## Question 6

![[Pasted image 20220927230204.png]]

An enterprise that uses private IP addresses can do so without coordination with IANA or an internet registry. Devices on the private IP addresses are unable to connect to hosts outside of the enterprise. 
LumiNUS uses public IP address.
When my laptop is connected, private IP addresses are used (DHCP to support mobile users)

## Network Address Translation (NAT)
- router maintains on external ip address
	- Each host on the same local network have the same external IP address
	- Router needs to store NAT table in memory