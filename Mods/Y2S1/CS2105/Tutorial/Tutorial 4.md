# Tutorial 4

## Question 1
[KR, Chapter 3, R6] Is it possible for an application to enjoy reliable data transfer even when the application runs over UDP? If so, how?

Yes. The application developer can put reliable data checking and recovery into the application layer protocol. (ACK, seq#, checksum, timeout, re-transmission, etc).


## Question 2
Show an example that if the communication channel between the sender and receiver can reorder messages (i.e. two messages are received in different order they are sent), then protocol rdt3.0 will not work correctly.

Assumptions about 3.0 is no packet reordering, flip bits, packet delay. For some reason, it takes a longer time than the timeout so the timeout is triggered. old packet 0 vs new packet 0.


## Question 3
[KR, Chapter 3, P29] It is generally a reasonable assumption, when sender and receiver are connected by a single wire, that packets cannot be reordered within the channel between the sender and receiver. However, when the “channel’ connecting the two is a network, packet reordering may occur. One manifestation of packet reordering is that old copies of a packet with a sequence or acknowledgement number of x can appear, even though neither sender’s nor receiver’s window contains x. With packet reordering, the channel can be thought of as essentially buffering packets and spontaneously emitting these packets at any point in the future. What is the approach taken in practice to guard against such duplicate packets?

The sender should not be able to send segments that are outside of the window until the segments within the window have been acknowledged. For example, for a window of 2, after sending packets 0, 1. It is unable to send packet 2 and 3 until acknowledgement has been sent from the reciever. 

Goal: to make sure that the sequence number is not reused until the sender is "sure" that any previously sent packets are different.

**Ans:**
First TCP use a large sequence number field (32 bits) to lower the chance that a sequence number cannot be reused.

Secondly, a packet cannot live in the network forever, fixed number of hops it can make. If TTL (time to live) field reaches zero, the router will discard this datagram.


## Question 4
[Modified from KR, Chapter 3, P37] Host A is sending data segments to Host B using a reliable transport protocol (either GBN or SR). Assume timeout values are sufficiently large such that all data segments and their corresponding ACKs can be received (if not lost in the channel) by Host B and the Host A respectively. Suppose Host A sends 5 data segments to Host B and the 2nd data segment is lost. Further suppose retransmission is always successful. In the end, all 5 data segments have been correctly received by Host B. How many segments has Host A sent in total and how many ACKs has Host B sent in total if either GBN or SR protocol is used? What are their sequence numbers? Answer this question for both protocols.

### GBN protocol
Host A segments: 9
Host B ACKs: 8

Host A:
pkt0
pkt1
pkt2
pkt3
pkt4
pkt1
pkt2
pkt3
pkt4

Host B:
ack0
ack0
ack0
ack0
ack1
ack2
ack3
ack4


### SR protocol
Host A segments: 6
Host B ACKs: 5

Host A:
pkt0
pkt1
pkt2
pkt3
pkt4
pkt1

Host B:
ack0
ack2
ack3
ack4
ack1


## Question 5
[KR, Chapter 3, R15] Suppose Host A sends two TCP segments back to back to Host B over a TCP connection. The first segment has sequence number 65; the second has sequence number 92.

a) 27 bytes

b) ack number will be 65 since it is expecting the first segment again. Note the TCP acknowledgement is cumulative.


## Question 6
[KR, Chapter 3, P26] Consider transferring an enormous file of L bytes from Host A to Host B. Assume an MSS of 512 bytes.

1. 2<sup>32</sup> bytes. Sequence number does not increase by 1 with each packet, but changes by the number of bytes sent.
2. Number of segments = 8388608
    Header fields = 64 bytes
    Total number of bytes added on = 8388608 * 64 bytes
					    = 536870912 bytes
     Transmitted data = data + header bytes = 4831838208 bytes
     Trasmit time = 4831838208 bytes * 8 bits / 155 * 10<sup>6</sup> = 249.4 seconds (4s.f.)

## Question 7

1. What is the IP address and TCP port number used by the client computer (source) that is transferring the file to gaia.cs.umass.edu?

IP address: 10.110.105.77
Source port: 55389

2. What is the IP address of gaia.cs.umass.edu? On what port number is it sending and receiving TCP segments for this connection?

IP address: 128.119.245.12
Destination Port: 80 (Http over TCP)


## Additional Qn
- Sender and receiver using Selective Repeat
- first and the last sequence numbers are k and k+3
- Let packet with sequence numbers i be p<sub>i</sub>

