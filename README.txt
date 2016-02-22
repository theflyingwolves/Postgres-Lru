1) Team Members
Mi Chengyi   (A0105494E)
Wang Kunzhen (A0105514U)

2) Description
2.1) Overview
We added a new struct named BufferListNode with pointers to prev and next. A BufferListNode object is a node in the linked list. We preallocated all the BufferListNodes in an array stored in StrategyControl. 

2.2) Highlight of changes

```C
// CS3223 
// Update the buffered accessed. If delete is true, we remove it from the linked list, depending on three cases. If delete is false, we see if the buffer is in the linked list and if yes, we move it to the front. Otherwise, we create a new node and add it to the front of the linked list. 
void StrategyUpdateAccessedBuffer(int buf_id, bool delete);
```

```C
// CS3223 
// Replace the clock replacement policy by LRU policy
volatile BufferDesc *StrategyGetBuffer(BufferAccessStrategy strategy, bool *lock_held);
```

```C
// CS3223 
// Calling StrategyUpdateAccessedBuffer with delete true
void StrategyFreeBuffer(volatile BufferDesc *buf);
```

```C
// CS3223 
// Added the size of the StrategyControl->LRUListNodes, which is NBuffers*sizeof(BufferListNode)
Size StrategyShmemSize(void);
```

```C
// CS3223 
// Allocate some more memory for StrategyControl->LRUListNodes and initialize each of the BufferListNode
void StrategyInitialize(bool init);
```

2.3) Observations
We are able to pass the testcases but when we ran the benchmark script, the server hanged and no output was written to lru.txt. We tried multiple times and were still not able to get output to lru.txt. 