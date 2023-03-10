# Network Security


## Network Security
- Confidentiality
	- Only sender, inteded receiver should "understand" m,essage contents

- Authentication
	- Sender, receiver want to confirm identity of each other

- Message integrity
	- Sender, receiver want to ensure message not altered without detection

- Access and availability
	- Services must be accessable and available to users

Involves encryption algorithms and decryption algorithms.

**Notation**
m: plaintext message
K<sub>A</sub>: Encryption algorithm, with key K<sub>A</sub> 
K<sub>B</sub>: Encryption algorithm, with key K<sub>B</sub> 


## Types of Cryptography
- Symmetric Key Cryptography
	- Sender and receiver use the *same key*
- Asymmetric Key Cryptography (aka public key cryptography)
	- Sender and receiver use *different key*



### Symmetric Key Cryptography
How does A and B agree on key value?
Will need to decide on the common key prior to communication via some other means


### Caesar's Cipher
- Substituting one thing for another
- Fixed shift of alphabet
- Only 25 possible values to shift numbers


### Monoalphabetic cipher
- Substitute one letter for another
- 26! mappings available
- susceptible to statistical analysis
	- knowing the occurances of letters that often appear together
- Intruder knows about some of the contents in the message
- Each letter has only one mapping
	- Solution: use multiple mappings
	- Define a cycling pattern
	- For each new plaintext symbol, use subsequent substitution pattern in cyclic pattern


### Breaking an encryption scheme
- *Ciphertext only attack:* Trudy has ciphertext she can analyze 
- *Known-plaintext attack:* Trudy has plaintext corresponding to ciphertext • e.g., in monoalphabetic cipher, Trudy determines pairings for a,l,i,c,e,b,o, 
- *Chosen-plaintext attack:* Trudy can get ciphertext for chosen plaintext


### Block Cyphers
- The message to be encrypted is processed in blocks of K bits
- if K=64, the message is broken into 64-bit blocks
- To encode a block, the cipher uses a one-to-one mapping
- *DES: Data Encryption Standard*
	- 54-bit symmetric key, 64-bit block
	- Can be brute forced in less than a day
- *AES Advanced Encryption Standard*
	- 128 bit blocks; 128, 192, 256 bit keys
	- Brute force that takes 1 second on DES takes 149 trillion years for 128-AES


## RSA
**Rivest, Shamir, Adleman algorithm**
- Only used for session keys


## Message Integrity
Ensure message is not altered without detection
- Checksum
- Parity
- CRC

Internet checksum
- produces fixed length digest (16-bit sum)
- is many-to-one
- easy to find another message with the same checksum value
- used to detect accidental errors rather than intentional changes

CRC
- Yet poor
- Ouput is biased to the input


### Cryptographic Hash Function
- Hash function
- Many-to-1
- takes in an input m and produces fixed-size msg digest
- Computationally infeasible to find any to different messages x and y such that H(x) = H(y)

- Both SHA-1 and MD5 are cryptographically broken
- Replaced by SHA-2 and SHA-3

**Message Integrity**
- The sender and receiver share a "Authentication key" s
- Send (m, H(m + s))
- This works as s is a secret key known to the receiver and no one else



## Digital Signatures
- Cryptographic technique analogus to hand-written signatures
- Signature must be:
	- Verifiable
		- Recepient can check the signature and the message was generated by sender
	- Unforgable
		- No one other than user should be able to generate the signature and the message

Sender signs m by encrypting with a private key K<sub>b</sub> creating the signature K<sub>b</sub>(m)
Alice receives messgae m with signature K<sub>b</sub>(m)
Alice verifies by using Bob's public key to check that it returns the message
So that means the whoever has signed m must have used bobs private key

Alice can verify that:
- Bob signed m
- No one else signed m
- Bob signed m and not m'
- Alice can take m and signature K<sub>b</sub>(m) to prove that the message has ben signed by BOB


### Opitmization
- Apply hash function H to get m, get fixed message size
- Bob will hash the message, then apply the signature to the hash K<sub>b</sub>(H(m))


### Public Key Certification
Problem: The reason we failed was because we did not know Bob's publc key
Solution:  We create a Certification authority(CA) who maintain a public database of everyone’s public key, Anyone who receives a message from “Bob” will access this database for 𝐾𝐵+ 

Problem: What if Trudy intercepts the communication with the CA and alters it? 
Solution: • CA signs it’s messages. 

Problem: We do not know CA’s public key 
Solution: Let us make this a universal knowledge!!! We maintain a list of CAs trusted a priori. Operating system has a list of “Trusted Root Certification Authorities


## Firewall
isolates organizations internal net from larger internet, allowing some packets to pass, blocking others

*Prevent denial of service (DoS) attacks:*
- SYN flooding: attacker establishes many bogus TCP connections, blocking resources for "real" connections

*Prevent illegal modifications/access of internal data*
- e.g., attacker replaces CIA's homepage with something else

*Allow only authorized access to inside network*
- set of authenticated users/hosts

Three types of firewalls:
- stateless packet filters
- stateful packet filters
- application gateways


### Stateless packet filtering
- internal network connected to Internet via router firewall
- Router filters packet-by-packet, decision to forward/drop packet based on:
	- source IP address, destination IP address
	- TCP/UDP source and destination port numbers
	- ICMP message type
	- TCP SYN and ACK bits

example, block all UDP inflow/outflow by blocking datagrams with IP protocol field 17
example, block inbound TCP segments with ACK=0, prevent external clients from making TCP connections with internal clients but allows internal clients to connect to outside

![[Pasted image 20221027223823.png | 500]]

### Access Control Lists
Table of rules applied top to bottom to incoming packets: (action, condition) pairs


### Limitations of firewalls
- IP spoofing: router cant really know if data comes from a claimed source
- can cause a bottleneck
- *tradeoff:* degree of communication with outside world, level of security
- Many highly protected sites still suffer from attacks

