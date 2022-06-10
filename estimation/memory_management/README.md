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
2. API function implementation:  
    1. __new(size: usize, id: i32): usize  - **5 days**  
    2. __renew(oldPtr: usize, size: usize): usize - **5 days**  
    3. __visit(ptr: usize, cookie: i32): void - **5 days** (*GC related*)
    4. __pin(ptr: usize): usize - **5 days** (*GC related*)  
    5. __unpin(ptr: usize): void - **5 days** (*GC related*)  
    6. __collect(): void - **10 days** (*GC related*)  
3. Unit Test and Integration test  **10 days**  

### Total  
**55** days, not sure if we still need some buffer to this task.  
