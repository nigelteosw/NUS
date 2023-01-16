# Caching 1

## Types of Memory

**SRAM**
- 6 transistors per memory cell
- Low density
- Fast access latency of 0.5 – 5 ns
- More costly
- Uses flip-flops


**DRAM**
- 1 transistor per memory cell
- High density
- Slow access latency of 50-70ns
- Less costly
- Used in main memory

### Use a hierarchy of memory technologies:
- Small but fast memory near CPU
- Large but slow memory farther away from CPU

### Temporal locality (time)
- If an item is referenced, it will tend to be referenced again soon

### Spatial locality (space)
- If an item is referenced, nearby items will tend to be referenced soon

- Different locality for
	- Instructions
	- Data

## Cache – a small but fast SRAM near CPU
- Hardware managed: Transparent to programmer


## Terminology
- **Hit: Data in cache** 
	- Hit rate: Fraction of memory accesses that hit
	- Hit time: Time to access cache
- **Miss: Data is not in cache**
	- Miss rate: 1 - Hit rate
	- Miss penalty: Time to replace cache block + hit time
- Hit time < Miss penalty

**Average Access Time**
= Hit rate * Hit Time + (1- Hit rate) * Miss penalty


## Cache Mapping
- Cache Block/Line
	- Unit of transfer between memory and cache

![[Pasted image 20221104203302.png | 500]]

Cache Block size = 2N bytes
Number of cache blocks = 2M
*Offset* =  N bits
*Index*  =  M bits
*Tag*     =  32 – (N + M) bits


Along with a data block (line), cache also contains the following administrative information (overheads):
1. Tag of the memory block
2. Valid bit indicating whether the cache line contains valid data


( Valid[index] = TRUE ) AND  ( Tag[ index ] = Tag[ memory address ] )


![[Pasted image 20221104203628.png | 500]]

![[Pasted image 20221104203957.png | 500]]


## Cache Misses
- **Compulsory misses**
	- First access to a block, the block must be brought into the cache
	- aka *cold start misses* or *first reference misses*
- **Conflict misses**
	- Occur in the case where several blocks are mapped to the same block/set
	- aka *collision misses* or *interference misses*
- **Capacity misses**
	- Occur when blocks are discarded as cache cannot contain all blocks needed


## Write Policy
- Cache and main memory are inconsistent
	- Modified data only in cache, not memory

**Write-through** cache
- Write data both to cache and main memory
- *Problem:*
	- Write will operate at the same speed of main memory
- *Solution:*
	- Put a write buffer between cache and main memory
		- Processor: writes data to cache + write buffer
		- Memory controller: write contents of the buffer to memory

**Write-back** cache
- Only write to cache
- Write to main memory only when cache block is replaced (evicted)
- *Problem:*
	- Quite wasteful if we write back every evicted cache blocks
- *Solution:*
	- Add an additional bit (Dirty bit) to each cache block
	- Write operation will change the dirty bit to 1 
		- Only cache block is updated, no write to memory
	- When a cache block is replaced:
		- Only write back to memory if dirty bit is 1


## Handling Cache Misses
- On a *Read Miss*
	- Data loaded into cache and then load from there to register

**Write allocate**
- Load the complete block into cache
- Change only the required word in cache
- Write to main memory depends on write policy

**Write around**
- Do not load the block to cache
- Write directly to the main memory


![[Pasted image 20221104210315.png | 500]]

