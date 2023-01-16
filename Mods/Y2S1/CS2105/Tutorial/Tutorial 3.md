# Tutorial 3

1) a) POST request
    b) A _POST request_ is typically sent via an HTML form and results in a change on the server.
    A _GET request_ is used to request data from a specified resource.

2) Yes, we can use dig to query that Web site in the local DNS server. Since a website that was just accessed a couple of seconds ago, will be  cached in the local DNS cache, the query time is much smaller. Else, it will take a much longer time to query the external Web site.

3) a) ConnectionRefusedError: [WinError 10061] No connection could be made because the target machine actively refused it.
   
   When creating a local socket, client will attempt to make a TCP connection to a non-existent server proess. Exception will be thrown.
   
    b) ConnectionResetError: [WinError 10054] An existing connection was forcibly closed by the remote host
    
    UDP client does not establich connection to server when creating local socket, hence it does not matter.

4) [KR, Chapter 3, R7]  
   For each received segment, at the socket interface, the IP addresses are provided by the operating system. Yes both will be directed to the same socket. Sock APIs are available for programmers to learn the IP address of the origin of the packet

5) a) Sum: 11000001
	checksum: 00111110
    b) Sum: 01000000
        checksum: 10111111

6) It will detect any single bit flip, but if the packet is altered such that the sum of all the data as 16 bit values remains constant, the checksum will not detect the error.
   
   

7) We needed to introduce sequence numbers as there might be ACK/NAK errors that may cause the server to send duplicate packet. By keeping track of the packets, the receiver will know which packet to discard.