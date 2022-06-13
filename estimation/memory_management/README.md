# Estimation for new Assembly Script Memory Management and GC Solution

## Memory Management

### Description
current Assembly Script MM solution is Two-Level Segregate Fit ([TLSF](http://www.gii.upv.es/tlsf/)).  
in addition, AssemblyScript will visit the tail position with follow structure.  
```
// ╒════════════════════ Block layout (32-bit) ════════════════════╕
//    3                   2                   1
//  1 0 9 8 7 6 5 4 3 2 1 0 9 8 7 6 5 4 3 2 1 0 9 8 7 6 5 4 3 2 1 0  bits
// ├─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┼─┼─┤            ┐
// │                          size                             │L│F│ ◄─┐ info   overhead
// ╞>ptr═══════════════════════════════════════════════════════╧═╧═╡   │        ┘
// │                        if free: ◄ prev                        │ ◄─┤ usize
// ├───────────────────────────────────────────────────────────────┤   │
// │                        if free: next ►                        │ ◄─┤
// ├───────────────────────────────────────────────────────────────┤   │
// │                             ...                               │   │ >= 0
// ├───────────────────────────────────────────────────────────────┤   │
// │                        if free: back ▲                        │ ◄─┘
// └───────────────────────────────────────────────────────────────┘ >= MIN SIZE
// F: FREE, L: LEFTFREE
```

As WebAssembly regard one memory page as 64K, so every time memery grow, it will visit the first part and latest part, which will cause confliction to CDC linear memory strategy.  

### estimation
1. Solution Determination (currently we want [RTOS](https://github.com/embeddedartistry/libmemory), but could change if it not fit our need) and primary POC preparing - **10 days**  
2. main feature:
    1. Memory management data structure design - **5 days**
    2. "initialize" and "growMemory" implementation - **5 days**
    3. "removeBlock" and "freeBlockMerge" implementation - **5 days**
    4. "searchBlock" implementation - **2 days**
    5. "prepareBlock" implementation - **2 days**  
3. API function implementation:  
    1. __alloc(size: usize): usize  - **2 days**  
    2. __realloc(ptr: usize, size: usize): usize - **3 days**  
    3. __free(ptr: usize): void - **2 days** (*GC related*)
    4. __shrink(size: usize): usize - **3 days** (*GC related*)  
4. Integration with GC functionality - **10 days**
5. Unit Test and Integration test  **5 days**  

### Total  
**54** days  
