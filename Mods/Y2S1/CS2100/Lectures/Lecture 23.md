# Caching 2

## Block Size Trade-off
**Larger block size:**
- Takes advantage of spatial locality
- Larger miss penalty: takes longer to fill up the block
- If block size is too big: too few cache blocks -> miss rate will go up


## Set-Associative (SA) Cache
**N-way Set Associative Cache**
- A memory block can be placed in a fixed number (N) of locations in the cache, where N > 1

**Key Idea:**
- Cache consists of a number of sets:
	- Each set contains N cache blocks
- Each memory block maps to a unique cache set
- Within the set, memory block can be placed in any of the N cache blocks in the set

- A memory block maps to a unique set
	- The memory block can be placed in either of the cache blocks

## Mapping
**Cache Set Index**
= (BlockNumber) module (NumberOfCacheSets)

![[Pasted image 20221104213311.png | 500]]


## Fully Associative (FA) Cache: Analogy
**Fully Associative Cache**
- A memory block can be placed in any location in the cache

**Key Idea:**
- Memory block placement is no longer restricted by cache index or cache set index
- Can be placed in any location but
- Need to search all cache blocks for memory access
- Only have offset and tag

**Least Recently Used (LRU)**
- How: For cache hit, record the cache block that was accessed
- When replacing a block, choose one which has not been access for the longest time
- Temporal locality
- Drawback
	- Hard to keep track if there are many choices
- Other replacement policies:
	- FIFO
	- RR
	- LFU (Least Frequently Used)