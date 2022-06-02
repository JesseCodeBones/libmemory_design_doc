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
free list is double linked list, it only contains `prev` and `next` element  
```
typedef struct ll_head
{
	/// Pointer to the next element in the list.
	struct ll_head* next;
	/// Pointer to the previous element in the list.
	struct ll_head* prev;
} ll_t;
```

## heap data structure
heap data structure contains ll_head, size information and data section:

typedef struct
{
	ll_t node;
	size_t size;
	char* block;
} alloc_node_t;


