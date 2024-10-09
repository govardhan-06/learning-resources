# Cache Mapping

## Direct Mapping

### Cache and Main Memory Specifications:
- **Cache size**: 128 blocks (lines) with each block containing 16 words.
    - Total words in cache = 128 blocks * 16 words = **2048 words (2K words)**.
  
- **Main memory size**: 64K words.
    - Main memory is divided into blocks, each of size 16 words.
    - Total number of blocks in main memory = 64K words / 16 words per block = **4K blocks** (or 4096 blocks).

### Direct Mapping:
In **direct-mapped cache**, each block of main memory maps to exactly one specific cache line based on a simple modulus operation. Specifically, **block 'j'** of the main memory will map to **cache line (j mod number of cache lines)**.

- Number of cache lines = 128.
- Thus, a block number \( j \) in main memory will be mapped to cache line \( j \mod 128 \).

For example:
- Main memory block 0, 128, 256, etc., will map to cache block 0.
- Main memory block 1, 129, 257, etc., will map to cache block 1.
- And so on, until block 127 of main memory, which will map to cache block 127.

After block 127, block 128 will wrap around and map back to cache block 0, and the process continues cyclically.

### Address Breakdown:
The processor generates a **16-bit address** to access the main memory, and this address is divided into three parts for the cache:

1. **Block Offset (4 bits)**: 
   - Since each block contains 16 words, you need 4 bits to select one of the 16 words within the block.
   - These 4 bits come from the least significant bits of the 16-bit address.

2. **Cache Block Index (7 bits)**:
   - The next 7 bits of the address specify which of the 128 cache blocks (lines) the main memory block will map to.
   - These bits are used to compute which cache block to access.

3. **Tag (5 bits)**:
   - The high-order 5 bits are used as a **tag** to distinguish between different main memory blocks that map to the same cache line.
   - The tag helps identify which of the 32 possible memory blocks (since \( 2^5 = 32 \)) is currently loaded in the corresponding cache line.

### Cache Lookup Process:
When a memory address is accessed:
1. The **block offset** (4 bits) is used to find the word within a block.
2. The **cache block index** (7 bits) determines the cache block to access.
3. The **tag bits** (5 bits) from the memory address are compared with the tag stored in the cache block to see if it matches. If the tag matches, it's a **cache hit**; otherwise, it's a **cache miss** and the block needs to be fetched from main memory.

### Key Points:
- The cache uses **direct mapping**, meaning there is a fixed correspondence between a main memory block and a cache line.
- No **replacement algorithm** is needed because any new block automatically replaces the previous block in the same cache line (if the new block maps to that line).
- **Cache misses** occur if the block needed is not present in the cache, in which case the corresponding main memory block must be fetched into the cache.

This design is simple and fast due to the direct mapping, but it can suffer from high conflict misses if multiple blocks frequently map to the same cache line.

Let's go through an example to explain the **direct-mapped cache** process using the given scenario.

### Cache and Memory Configuration Recap:
- **Cache**: 128 blocks (lines), each block with 16 words.
- **Main Memory**: 64K words, organized into 4096 blocks (4K blocks), with each block containing 16 words.
- **Address size**: 16 bits.

### Example: Mapping Main Memory Blocks to Cache Lines

Suppose you want to access **memory address 34567 (decimal)**. Let's break down the process of mapping this address to the cache.

#### Step 1: Convert the Memory Address to Binary
Memory address \( 34567_{10} \) in binary is:
\[ 34567_{10} = 1000011100001111_2 \]

This 16-bit address can be divided into three parts:
1. **Block Offset** (low-order 4 bits): Selects the specific word within a block.
2. **Cache Block Index** (next 7 bits): Determines the cache block (line) to map the main memory block to.
3. **Tag** (high-order 5 bits): Distinguishes between multiple main memory blocks that map to the same cache block.

Let's divide the address into these parts:

- **Block Offset**: The least significant 4 bits are `1111`. This means we want the 16th word within the block (since words are numbered from 0 to 15).
- **Cache Block Index**: The next 7 bits are `0111000`, which is 56 in decimal. This means the block will map to **cache line 56**.
- **Tag**: The remaining 5 bits are `10000`, which will be stored as the tag for this block.

#### Step 2: Access the Cache
Now, let's see what happens when you access the cache:

1. **Determine the Cache Block**:
   - The **Cache Block Index** is 56, so you will check **cache line 56**.

2. **Check the Tag**:
   - In cache line 56, you compare the **Tag** stored in that line with the **Tag** from the memory address (`10000`).
   - If the tags match, it's a **cache hit**, and the word at the block offset `1111` (16th word) is accessed.
   - If the tags don’t match, it’s a **cache miss**, and the corresponding main memory block (in this case, the block containing address 34567) is fetched into **cache line 56**.

#### Step 3: Loading a Block in Case of Cache Miss
Suppose the block corresponding to address 34567 is not in the cache (cache miss). Here’s what happens:

1. The block from **main memory** that contains address 34567 is fetched into **cache line 56**. The block is block number \( \text{block number} = \frac{34567}{16} = 2160 \) (because there are 16 words per block).
   
2. The tag bits `10000` are stored in cache line 56 to indicate that block 2160 of main memory is now in this cache line.

3. When future accesses to memory addresses within this block occur, as long as they map to cache line 56 and have the same tag (`10000`), it will result in a **cache hit**.

### Another Example with Conflict

Now, let’s access **memory address 56047 (decimal)** and see what happens.

#### Step 1: Convert the Address to Binary
Memory address \( 56047_{10} \) in binary is:
\[ 56047_{10} = 1101101010011111_2 \]

Breaking it into parts:
- **Block Offset**: `1111` (low-order 4 bits, selects the 16th word in the block).
- **Cache Block Index**: `0100111` (next 7 bits, which is 39 in decimal).
- **Tag**: `11011` (high-order 5 bits).

#### Step 2: Access the Cache
1. The **Cache Block Index** is 39, so we look at **cache line 39**.
2. The tag bits `11011` are compared with the tag stored in cache line 39.

If the tag matches, it’s a **cache hit**. If not, it’s a **cache miss**, and the block containing address 56047 from main memory is loaded into **cache line 39**, replacing any block already stored there.

This shows that any memory block can map to only one cache line, and if two blocks map to the same line, they will replace each other, potentially causing **cache conflicts** (e.g., frequent replacements between two competing blocks).

### Recap of Direct Mapping:

- **Block 2160** (which contains memory address 34567) is stored in **cache line 56** with a tag `10000`.
- **Block 3502** (which contains memory address 56047) is stored in **cache line 39** with a tag `11011`.
  
Each memory block can map to only one cache line, determined by the **cache block index**.

Direct mapping is a caching technique used in computer architecture to efficiently store and retrieve data from a cache memory. Here’s a detailed explanation of direct mapping, particularly in the context of the provided memory and cache configuration.

### Basic Concepts of Caching:
1. **Cache Memory**: A smaller, faster type of volatile memory located close to the CPU. It stores frequently accessed data and instructions to reduce the average time to access data from the main memory (RAM).

2. **Cache Block (or Cache Line)**: A unit of data transferred between the cache and main memory. Each block holds a fixed number of bytes (or words).

3. **Mapping Function**: This determines how data from main memory is assigned to cache locations. Different mapping techniques include direct mapping, associative mapping, and set-associative mapping.

### What is Direct Mapping?
In direct mapping, each block in main memory maps to exactly one cache line. This means that for every address in the main memory, there is a specific location in the cache where that address can be stored. Here’s how it works in more detail:

#### 1. **Address Structure**:
In the case of direct mapping, a memory address is typically divided into three parts:
- **Tag**: Used to identify whether the data currently in the cache line corresponds to the requested memory address.
- **Index**: Determines which cache line to check for data. This is derived from the memory address.
- **Offset**: Indicates the specific byte or word within a cache line.

In your example:
- **Total address size**: 16 bits
- **Tag size**: 6 bits
- **Index size**: 8 bits
- **Offset size**: 2 bits

#### 2. **Mapping Process**:
When the CPU wants to read or write data, it generates a memory address:
1. **Extract the Index**: The index bits are used to determine which cache line to look at.
2. **Check the Tag**: The tag bits are compared against the tag stored in that cache line to see if the data is valid.
3. **Access the Data**:
   - If the tags match (a **cache hit**), the CPU retrieves the data from the cache line.
   - If the tags do not match (a **cache miss**), the CPU fetches the data from main memory and updates the cache line with the new data, also updating the tag.

#### 3. **Example**:
Let’s assume you have a memory address (in binary):
```
A = 00000000 00000000
```
In this case:
- The last 2 bits are used for the **offset** (selecting one of 4 words).
- The next 8 bits are for the **index**, which determines which of the 256 cache blocks to access.
- The first 6 bits represent the **tag**.

When the CPU accesses the address:
1. It computes the cache line index from the address (using the index bits).
2. It checks the cache line at that index for a valid tag.
3. Depending on whether the tag matches or not, it either retrieves the data from the cache or loads it from memory into the cache.

### Advantages and Disadvantages:
- **Advantages**:
  - **Simplicity**: Direct mapping is straightforward to implement because each block in memory has a specific location in the cache.
  - **Fast Access**: Access times are fast since only one cache line needs to be checked.

- **Disadvantages**:
  - **Conflict Misses**: Multiple memory addresses can map to the same cache line (i.e., if they differ in the tag but have the same index). This can lead to higher cache miss rates, especially if frequently accessed data is mapped to the same line.
  - **Limited Flexibility**: If many blocks compete for the same cache line, it can lead to inefficient use of cache.

### Conclusion:
In summary, direct mapping is a simple and effective way to manage cache memory, but it may lead to inefficiencies due to conflict misses. Understanding how direct mapping works helps in optimizing cache performance and system efficiency in computer architecture.

# Set-Associative Mapping

In a cache memory system, addresses from main memory are divided into three fields: **tag**, **index**, and **offset**. Each of these fields plays a crucial role in determining where data is stored in the cache and how it can be accessed. Let’s break down these components and illustrate them with an example.

### 1. Address Breakdown

When a CPU generates a memory address, it typically consists of multiple bits. For example, consider a scenario where we have:

- **Main Memory Size**: 128 KB (which is \(128 \times 1024 = 131072\) bytes)
- **Cache Size**: 16 KB (which is \(16 \times 1024 = 16384\) bytes)
- **Block Size**: 256 bytes

**Total Number of Blocks in Cache:**
\[
\text{Total Cache Blocks} = \frac{\text{Cache Size}}{\text{Block Size}} = \frac{16384}{256} = 64 \text{ blocks}
\]

**Number of Sets in Cache:**
Assuming a 2-way set associative cache:
\[
\text{Number of Sets} = \frac{\text{Total Cache Blocks}}{\text{Number of Ways}} = \frac{64}{2} = 32 \text{ sets}
\]

### 2. Address Fields

**Bits Required:**
- **Physical Address Size**: The size of the main memory (128 KB) means we need \( \log_2(128 \times 1024) = 17 \) bits for the physical address.
- **Offset**: Since each block is 256 bytes, the number of bits needed for the offset is:
  \[
  \text{Offset bits} = \log_2(256) = 8 \text{ bits}
  \]
- **Index**: With 32 sets, the index field needs:
  \[
  \text{Index bits} = \log_2(32) = 5 \text{ bits}
  \]
- **Tag**: The remaining bits in the address will form the tag:
  \[
  \text{Tag bits} = \text{Total Address bits} - (\text{Index bits} + \text{Offset bits}) = 17 - (5 + 8) = 4 \text{ bits}
  \]

### 3. Example of Address Breakdown

Let’s take a hypothetical memory address in binary format: **10101010101010101** (17 bits).

**Address Format:**
- **Tag**: 4 bits
- **Index**: 5 bits
- **Offset**: 8 bits

**Example Address Breakdown**:
Assuming the binary address is:
```
Tag | Index | Offset
1110 | 01010 | 00000001
```
- **Tag (1110)**: This identifies which block of main memory is stored in the corresponding cache set. It acts as a unique identifier for that specific block of memory.
- **Index (01010)**: This points to the cache set (in this case, set 10) where the data may reside. For a 2-way set associative cache, this set can contain 2 different blocks of memory.
- **Offset (00000001)**: This specifies the particular byte within the 256-byte cache line. The offset is needed to locate the exact byte requested from the block stored in the cache.

### 4. Cache Lookup Process

When the CPU needs to access data at this memory address:
1. **Extract Fields**: The cache controller extracts the tag, index, and offset from the address.
2. **Index Lookup**: It uses the index to determine which cache set to check.
3. **Tag Comparison**: In the chosen set, it compares the tag of each block with the tag extracted from the address to determine if the desired block is present in the cache (cache hit).
4. **Data Access**: If there is a match (hit), the data is accessed using the offset. If there’s no match (miss), the block is fetched from main memory, stored in the cache (possibly replacing one of the existing blocks), and then the requested data is accessed using the offset.

### Summary

- **Tag**: Uniquely identifies a memory block stored in the cache.
- **Index**: Indicates the specific set within the cache.
- **Offset**: Points to the specific byte within a cache line.

This structured approach allows caches to operate efficiently, reducing access times and improving overall system performance.
