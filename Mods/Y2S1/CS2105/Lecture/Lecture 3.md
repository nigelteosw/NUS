# Domain Name System#

Two ways to identify a host:
1) Hostname: www.example.org
2) IP address: 93.184.216.34

HTTP uses **TCP** as a transport service
- TCP, in turn, uses service provided by the **IP**!

## DNS: Resource Records##
Mapping between host names and IP address
RR format: (name, value, type, ttl)

### Types###
- A
	- name is hostname
	- value is IP address
- CNAME
	- name is an alias name, there will be some canonical name
	- value is canonical name
- NS
	- name is domain
	- value is hostname of authoritative name server for this domain
- MX
	- value is name of mail server associated with name

DNS stored RR in distrbuted databases implemented in heirarchy of many name servers.

## Root Servers##
Root-level servers
Top-level domain (TLD) servers
Authoritative-level servers

Contact local DNS Server to make webpage lookup faster
DNS Caching
- cached entries may be out-of-date
- cached entries expire after some time (TTL)
- if name host changes IP address, may not be known Internet-wide until all TTLs expire
- DNS runs over **UDP**
- DNS Name Resolution usually using **iterative query**

## SOCK_STREAM and SOCK_DGRAM##
TCP almost always uses `SOCK_STREAM` and UDP uses `SOCK_DGRAM`.

TCP (`SOCK_STREAM`) is a connection-based protocol. The connection is established and the two parties have a conversation until the connection is terminated by one of the parties or by a network error.

[[UDP]] (`SOCK_DGRAM`) is a datagram-based protocol. You send one datagram and get one reply and then the connection terminates.

-   If you send multiple packets, TCP promises to deliver them in order. UDP does not, so the receiver needs to check them, if the order matters.
-   If a TCP packet is lost, the sender can tell. Not so for UDP.
-   UDP datagrams are limited in size, from memory I think it is 512 bytes. TCP can send much bigger lumps than that.
-   TCP is a bit more robust and makes more checks. UDP is a shade lighter weight (less computer and network stress).