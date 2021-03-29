---
layout: notes
title: "[Data Structures] Priority Queues"
meta: Implementation of Priority Queues
reference: Loudon, K. (1999). Mastering Algorithms with C. O'Reilly Media, Inc.
category: data-structures
---

## Header for the Priority Queue Abstract Datatype

```c
/* 
 * File Name    : pqueue.h
 * Description  : Header for the Priority Queue Abstract Datatype
 * Reference    : Loudon, K. (1999). Mastering Algorithms with C. O'Reilly
                  Media, Inc.
 */

#ifndef PQUEUE_H
#define PQUEUE_H

#include "heap.h"

/* Implement priority queue as heaps. */
typedef Heap PQueue;

/* Public Interface */
#define pqueue_init heap_init
#define pqueue_destroy heap_destroy
#define pqueue_insert heap_insert
#define pqueue_peek(pqueue) ((pqueue)->tree == NULL ? NULL : (pqueue)->tree[0])
#define pqueue_size heap_size

#endif
```