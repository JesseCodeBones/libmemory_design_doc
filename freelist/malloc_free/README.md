# malloc add block

## align address

num: address number
align: size of void*

```c
#ifndef align_up
#define align_up(num, align) (((num) + ((align)-1)) & ~((align)-1))
#endif
```
## prepare free list
all free block are stored at free_list linked list.  
it is a static variable stored at program space.




