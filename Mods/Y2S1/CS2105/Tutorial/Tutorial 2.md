# Tutorial 2

1) Consider the following HTTP request message sent by a browser. 
GET /index.html HTTP/1.1 
Host: www.example.org 
Connection: keep-alive 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36 
Accept-Encoding: gzip, deflate

a) www.example.org/index.html
host + resource location
b) HTTP/1.1
c) Persistent connection
under the connection: keep-alive not closed
d) IP Address is not shown in the HTTP request. One would be able to get the information from the socket

2) The text below shows the header of the response message sent from the server in reply to the HTTP GET message in Q1 above. Answer the following questions. 

HTTP/1.1 200 OK 
Content-Encoding: gzip 
Content-Type: text/html; charset=UTF-8 
Date: Wed, 23 Jan 2019 13:50:31 GMT Page 2 of 4 
Last-Modified: Fri, 09 Aug 2013 23:54:35 GMT 
Connection: Keep-Alive 
Content-Length: 606

a) Yes (message was 200 OK)
b)  Wed, 23 Jan 2019 13:50:31 GMT
c) 606
d) Yes (Keep-Alive)

3) True or false?

a) False, download one object per request.
Pipelining means we don't have to wait for the request.
b) True – *If the connection did not timeout, then it can be used to send another html request over the same port* 
c) False, the Date header is the date and time the message was sent.
Instead, we must look for another header field 'Last-Modified'
d) True - the HTTP response code must always be returned

4) [Modified from KR, Chapter 2, P7]
RTT = Round-trip Time
n dns servers
D<sub>DNS</sub> RTT time 
m small objects
D<sub>Web</sub> RTT between local host and the server of each object

n * D<sub>DNS</sub> to get IP address  
2 * (m + 1) * D<sub>Web</sub> for each item
Ans =  n * D<sub>DNS</sub> + 2 * (m + 1) * D<sub>Web</sub>

5) [Modified from KR, Chapter 2, P8]

a) Ans =  3 * D<sub>DNS</sub> + 2 * 6 * D<sub>Web</sub> = 
	 3 * D<sub>DNS</sub> + 12 * D<sub>Web</sub>
b) Ans = 3 * D<sub>DNS</sub> + 2 *  D<sub>Web</sub> + 2 * 2 * D<sub>Web</sub>
	= 3 * D<sub>DNS</sub> + 3 * 2 * D<sub>Web</sub>
c) Ans = 3 * D<sub>DNS</sub> + 2 *  D<sub>Web</sub> +  D<sub>Web</sub>
	no need handshake again due to pipelining
1) Do you know what is DNS cache poisoning? 

DNS cache poisoning **occurs when a threat actor feeds false information into the DNS cache, thereby making a user's web browser return an incorrect response**. This response usually redirects users to a website other than the one they intended to view.

An attacker adds fraudulent IP address information in the DNS cache, thereby making the DNS resolver call up the malicious site instead of the original one.

7) Wireshark Introduction
8) a) HTTP/1.1 200 OK 
    b) Last-Modified: Wed, 31 Aug 2022 05:59:02 


**For Questions 4 and 5**
![[Pasted image 20220901001712.png]]

Additional Question
HTML file 200 bytes (B)
Image file is 1000 bytes (B)
Client connected to Web server through a link of 1 Mbps
RTT is 100ms

Persistent HTTP with pipelining: 
Handshake: 100ms
HTML: 100ms (D<sub>prop</sub>) + 200 * 8 / 10<sup>6</sup> (D<sub>trans</sub>) = 101.6
IMG: 100ms + 5 * 1000 * 8 / 10<sup>6</sup> = 14.0
Total = 341.6ms

Persistent HTTP with no parallel requests:
Handshake: 100ms
HTML: 100ms (D<sub>prop</sub>) + 200 * 8 / 10<sup>6</sup> (D<sub>trans</sub>) = 101.6
IMG: (100 + 1000 * 8 / 10<sup>6</sup>) * 5

Non-persistent HTTP with no parallel TCP:
HTML: 100ms + 100ms + 1.6 = 201.6ms
IMG = (100ms + 100ms + 8ms) * 5
Ans = 1241.6

Non-persistent HTTP with max 3 parallel TCP:
HTML: 100ms + 100ms + 1.6 = 201.6ms
IMG1: 100ms + 100ms + 8ms * 3
IMG2: 100ms + 100ms + 8ms * 2 