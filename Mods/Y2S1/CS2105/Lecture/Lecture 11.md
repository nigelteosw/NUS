# Multimedia Networking

## 3 Application Types

**Streaming stored** audio video
- Streaming: can begin playout before downloading entire file
- Stored (at server/ CDNs): can transmit faster than audio/video will be rendered (implies storing/buffering at client) i.e. YouTube, Netflix

**Conversational ("two-way live")** voice/video over IP
- Interactive nature of human-to-human conversation limits delay tolerance (400 ms)

**Streaming live ("one-way live")** audio, video (not included in this module)
- Typically done with CDNs

## Multimedia: video

- Video: sequence of images displayed at constant rate
	- 30 img/sec
- Digital image: array of pixels
	- each pixel represented by bits
- Most salient characteristic of video is its high bit rate
- To reduce data usage, we compress the video
	- Use redundancy within and between images to decrease # bits used to encode image
	- *Spatial Coding* (within image)
	- *Temporal Coding* (from one image to next)

**CBR: (constant bit rate):** video encoding rate fixed
- Not responsive to the complexity of the video
- Need to set bitrate relatively high to handle more complex segments of video
- Consistency of CBR makes it well-suited for real time encoding
	- For *real time live streaming*

**VBR: (variable bit rate):** video encoding rate changes as amount of spatial, temporal coding changes
- VBR best suited for *on-demand video* due to longer time to process the data

**examples:**
- MPEG 1 (CD-ROM) 1.5Mbps
- MPEG2 (DVD) 3-6 Mbps
- MPEG4/H264 (used on Internet, < 2Mbps)
- H.265, 4K video > 10 Mbps

## Multimedia: audio
- Analog audio signal
	- sampled at constant rate
		- Telephone: 8000 samples/sec
		- CD music: 44100 samples/sec

- each sample quantized, i.e. rounded
	- each quantized value represented by bits, e.g. 8 bits for 256 values
	- 8000 samples/sec, 256 quantized values (8 bits) = 64000 bps
	- receiver converts bits back to analog signal (DAC):

*example rates*
- CD: 1.411 Mbps
- MP3: 96, 128, 160 kbps
- Internet telephony: 5.3 kbps and up


## Streaming Stored Video
**Streaming stored** video
- Streaming: Can begin playout before downloading entire file

**Stored (at server/CDNs):** can transmit faster than audio/video will be rendered (implies storing/buffering at client)


### Continous playout constraint
- once client playout begins, playback must match original timing
- but network delays are variables

- other challenges
	- client interactivity, pause, fast-forward, rewind 
	- video packets may be lost, retransmitted

- *client-side buffering and playout delay:* compensate for network-added delay, delay jitter

Ensure that buffer fill level is not empty
- If fill rate less than playout rate, buffer eventually empties
- If fill rate more tahn playout rate, buffer will not empty provided initial playout delay is large enough to absorb the variable fill rate
	- buffer starvation less likely with larger delay
	- but larger delay until user begins watching


## Streaming multimedia: UDP
- server sends at rate appropriate for client
	- send rate = encoding rate = constant rate
	- *push-based* streaming (server push)
	- UDP has no congestion control
		- transmission without rate control restrictions

- Short playout delay (2-5 secs) to remove network jitter
- Error recovery: application-level, time permitting

- Video chunks encapsulated using RTP (Real Time Protocol)
- Control Connection is maintained separately using RTSP (Real time Streaming protocol)
	- Is used for establishing and controlling media sessions between endpoints
	- Clients issue commands such as play record and pause
- Drawbacks
	- Need for a separate media control server like RTSP increases cost and complexity
	- UDP may not go through firewalls

## Streaming multimedia: HTTP
- multimedia filed retrieved via HTTP GET, pull-based streaming
- send at maximum possible rate under TCP

**Advantages**
- HTTP/TCP passes more easily through firewalls
- Network infrastructure (like CDNS and Routers) fine tuned for HTTP/TCP

**Drawbacks**
- fill rate fluctuates due to TCP congestion control, retransmission (in-order delivery)


## Voice-Over-IP
VoIP *end-to-end-delay* requirement: needed to maintain "conversational" aspect
- Higher delays noticeable, impair interactivity
	- < 150 msec: good
	- > 400 msec: bad
	- includes application-level (packetization, playout), network delays

Data loss over 10% makes conversation unintelligible

### Challenge
- Internetn (IP layer) is a *best-effort* service
	- no upper bound on delay
	- no upper bound on percentage of packet loss


### VoIP characteristics
- Speaker's audtio
	- alternating talk spurts, silent periods
	- pkts generated only during talk spurts
	- 20 msec chunks at 9 Kbytes.sec: 160 bytes of data

- application-layer header added to each chuk
- *chunk+header* encapsulated into UDP or TCP segment


**Network loss**
- IP datagram lost due to network congestion

**Delay loss**
- IP datagram arrives too late for playout at receiver
	- delays: processing, queueing in network; end-system (sender, receiver) delays
	- typical maximum tolerable delay: 400 ms
	- VoIP Applications usually use UDP to avoid Congestion Control
	- Loss tolerance, packet loss between 1% to 10% can be tolerated


**Delay jitter**
- end-to-end delays of two consecutive packets: difference can be more or less than 20 msec (transmission time difference)
- receiver attempts to playout each chunk exactly q msecs after chunk was generated
	- Tradeoff:
		- large q: less packet loss
		- small q: better interactive experience

**goal:** low playout delay, low late loss rate
**approach:** adaptive playout delay adjustment by estimating network delay
- silent periods compressed and elongated
	- chunks stil played out every 20 msec during talk spurt

### Adaptive playout delay
- Adaptive estimate packet delay (EWMA (exponentially weighted moving average))

![[Pasted image 20221030005341.png | 500]]


**Challenge:** recover from packet loss given small tolerable delay between original transmission and playout
- use ACK/NAK
	- each ACK/NAK takes ~ one RTT which is too slow

**Simple FEC**
- for every group of n chunks
	- create redundant chunk by XOR-ing n original chunks
	- send n + 1 chunks
- can reconstruct original n chunks if at most one lost chunk from n + 1 chunks with playout delay

*Drawback*
- Increasing bandwith by factor 1/n
- Playout delay is increased during packet loss


**Piggyback FEC**
"piggyback lower quality stream"

- send lower resolution audio stream as redundant information
- non-consecutive loss: receiver can conceal loss

- generalization: can also append (n-1)st and (n-2)nd low-bit rate chunk


**Interleaving to conceal loss:**
- Audio chunks divided into smaller units
- packet contains small units from different chunks
- if packet loss, still have most of every original chunk
	- concealed by packet repetition or interpolation
- no redundancy overhead, but increases playout delay even without error

![[Pasted image 20221030010326.png | 500]]



## Dynamic Adaptive Streaming over HTTP
- *Video-on-Demand* video streaming increasingly uses HTTP streaming
	- Simple HTTP streaming just GETs a (whole) video file from an HTTP server
- Drawbacks
	- can be wasteful, needs larger client buffer
	- all clients recieve the same encoding of video

**Server:**
- divides video file into multiple chunks
- each chunk stored, encoded at different rates
- *manifest file* provides URLs for different encodings

**Client:**
- periodically measures server-to-client bandwith
- consulting manifest, requests maximum coding rate sustainable given current bandwith
- can choose different coding rates at different points in time (depending on available bandwith at time
- when to request chunk
- what encoding rate to request
- where to request chunk

- Data is encoded into differen qualities and cut into *short segments*
- Client first downloads Manifest File, which describes the available videos and qualities
- Client/player executes an adaptive bitrate algorithm to determine which segment to download next

### Advantages
- Server is simple, regular web server
- No firewall problems
- Standard (image) web caching works

### Disadvantages
- DASH is based on media segment transmissions, typically 2-10 seconds in length
- By buffering segments at the client side, DASH does not provide low latency for two way conferencing


*challenge:* how to strean content to hundreds of thousands of simulataneous users

Store/serve multiple copies of videos at multiple geographically distributed sites (CDN)
CDN (Content distribution networks)
- enter deep: push CDN servers deep into many access networks
	- close to users
- bring home: smaller number of larger clusters in Internet exchange points near access networks


