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
```c
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

```c
typedef struct
{
	ll_t node;
	size_t size;
	char* block;
} alloc_node_t;
```

![image](https://user-images.githubusercontent.com/56120624/171594479-f31313f6-e781-49ba-a45e-7c81f47b7811.png)

## add block  
add block support multi add action.  
function: `void malloc_addblock(void* addr, size_t size)`

## malloc
* search free list, find suitable block (o(n))  
* check if this free block can be divide into two part  
* delete this block from free list
* return ptr  

## free
* find block with ptr
* add block into free list
* do block merge if neccessary

