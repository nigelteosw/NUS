# Application Layer 

## Client-Server Architecture ##
### Server: ###
- Waits for requests
- Provides requested service to client
- Data centres

### Client: ###
- Initiates contact with server
- Typically requests serivce from server

## P2P Architecture ##
- No always-on server
- e.g. Bit Torrent
- Peers request services from another peer
	- Self scalability - new peers bring in new service capacity
- Difficult to manage (users join and leave dynamically)
- Data integrity


## What transport serrvice does an app need? ##
### Data Integrity ###
- some applications require 100% reliable data transfer

### Throughput ###
- some applications require minimum bandwith to be effective (streaming service)

### Timing ###
- some applications require low delay for it to be "effective" (games)

### Security ###
- encryption, data integrity

## Transport Layer Protocols ##
### TCP service: ###
- Reliable data transfer
- flow control
- congestion control
- does not provide: timing minumum throughput, security

### [[UDP]] service: ###
- Unreliable data transfer
- no flow control
- no congestion control
- does not provide: timing minumum throughput, security
- Multiplexing at sender: UDP gathers data from processes, forms packets and passes them to IP
- De-multiplexing at receiver: UDP receives packets from lower layer and dispatches them to the right processes

## Application Layer Protocol ##
Web page usually consists of:
- base HTML file
- several referenced object
	- addressable by a URL

### HTTP Overview ###
- HyperText Transfer Protocol
- HTTP uses TCP as transport service
- Non-persistent HTTP (1.0)
- Persistent HTTP (1.1)

 ![[Pasted image 20220816105009.png]]
 ![[Pasted image 20220816105022.png]]

## Example HTTP Request Message ##
```http
GET /index.html HTTP/1.1\r\n Host: www.example.org\r\n Connection: keep-alive\r\n
```
![[Pasted image 20220816114359.png]]

