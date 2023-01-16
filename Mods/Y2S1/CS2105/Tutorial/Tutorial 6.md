# Tutorial 6

## Question 1

a) Give an example IP address assignment to all interfaces in this home network.
192.168.1.2, 192.168.1.3, 192.168.1.4 with the router interface being 192.168.1.1

b) Suppose each host has two ongoing TCP connections, all to port 80 of a server at 128.119.40.86. Provide example corresponding entries in the NAT translation table.

NAT Translation Table
| WAN side | LAN side |
| -----------| -----------|
| 24.34.112.235, 3000 | 192.168.1.2, 3213 |
| 24.34.112.235, 4000 | 192.168.1.2, 3214 |
| 24.34.112.235, 5000 | 192.168.1.3, 3215 |
| 24.34.112.235, 6000 | 192.168.1.3, 3216 |
| 24.34.112.235, 7000 | 192.168.1.4, 3217 |
| 24.34.112.235, 8000 | 192.168.1.4, 3218 |

port numbers on the lan side can be same as long as they are from different devices

## Question 2

a) How many fragments will be generated?
4 fragments

b) What is the length of each fragment (including IP header)?
500 + 500 + 500 + 60

c) What are the values of identification number, offset and flag in each fragment?
1. length = 500, id = 422, offset = 0, flag = 1
2. length = 500, id = 422, offset = 60, flag = 1
3. length = 500, id = 422, offset = 120, flag = 1
4. length = 60 id = 422, offset = 180, flag = 0


## Question 3

| | cost to w | cost to x | cost to y | cost to z |
|--|------|------|-----|-----|
|from x|3|0|3|5|
|from y|6|3|0|2|
|from z|8|5|2|0|


## Question 4

1. Within the IP packet header, what is the value in the upper layer protocol field?
Within the header, the value in the upper layer protocol field is ICMP (0x01)

2. Which fields in the IP datagram always change from one datagram to the next within this series of ICMP messages sent by your computer?
The fields that change:
- Checksum
- Identifier
- Time to Live (TTL)
- Source Address
- Destination Address