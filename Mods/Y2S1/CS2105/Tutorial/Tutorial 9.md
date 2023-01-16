# Tutorial 9

## Question 1
a) this is a secret message -> uasi si m icbocu hciimzc

b) tcow ihmou -> very smart


## Question 2
a) to use symmetric key encryption, number of keys needed is n(n-1)/2 as each pair has to share a key

b) for public key encryption, each person has a public and private key hence there are 2N keys


## Question 3
1. The MAC (Message Authentication Code) is used by each peer by each having a secret key and computing the hash h = H(m + s)
2. Sending the block (m, h) to another peer
3. If the peer receives the message (m, h) it should compute the hash H(m + s) and compare it to h = H(m + s)
	1. If the two hashes are the same, it accepts the blocks
	2. Else if the hashes are not the same, it rejects the blocks


## Question 4
Bob has to use his own private key to get the session key, using the session key Ks to decrypt the data sent by Alice.. get the message, and decrypt KA(H(m)) using Alice's public key to get H(m), then use the cryptographic hash function H on m, to get H(m) then compare both of them. If H(m) is equal to the H(m) done by Bob, then the message has been crafted by Alice.