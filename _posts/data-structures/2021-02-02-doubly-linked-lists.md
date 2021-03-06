---
layout: notes
title: "[Data Structures] Doubly-Linked Lists"
meta: Implementation of the Doubly-Linked Lists
reference: Loudon, K. (1999). Mastering Algorithms with C. O'Reilly Media, Inc.
category: data-structures
---

## Header for the Doubly-Linked List Abstract Datatype

```c
/* 
 * File Name    : dlist.h
 * Description  : Header for the Doubly-Linked List Abstract Datatype
 * Reference    : Loudon, K. (1999). Mastering Algorithms with C. O'Reilly
 *                Media, Inc.
 */

#ifndef DLIST_H
#define DLIST_H

#include <stdlib.h>

/* Define a structure for doubly-linked list elements. */
typedef struct DListElmt_
{
    void                *data;
    struct DListElmt_   *prev;
    struct DListElmt_   *next;
} DListElmt;

/* Define a structure for doubly-linked lists. */
typedef struct DList_
{
    int         size;
    int         (*match)(const void *key1, const void *key2);
    void        (*destroy)(void *data);
    DListElmt   *head;
    DListElmt   *tail;
} DList;

/* Public Interface */
void dlist_init(DList *list, void (*destroy)(void *data));
void dlist_destroy(DList *list);
int dlist_ins_next(DList *list, DListElmt *element, const void *data);
int dlist_ins_prev(DList *list, DListElmt *element, const void *data);
int dlist_remove(DList *list, DListElmt *element, void **data);
#define dlist_size(list) ((list)->size)
#define dlist_head(list) ((list)->head)
#define dlist_tail(list) ((list)->tail)
#define dlist_is_head(element) ((element)->prev == NULL ? 1 : 0)
#define dlist_is_tail(element) ((element)->next == NULL ? 1 : 0)
#define dlist_data(element) ((element)->data)
#define dlist_next(element) ((element)->next)
#define dlist_prev(element) ((element)->prev)

#endif
```

## Implementation of the Doubly-Linked List Abstract Datatype

```c
/* 
 * File Name    : dlist.c
 * Description  : Inplementation of the Doubly-Linked List Abstract Datatype
 * Reference    : Loudon, K. (1999). Mastering Algorithms with C. O'Reilly
 *                Media, Inc.
 */

#include <stdlib.h>
#include <string.h>

#include "dlist.h"

/* dlist_init */
/* Complexity: O(1) */
void dlist_init(DList *list, void (*destroy)(void *data))
{
    /* Initialize the list. */
    list->size = 0;
    list->destroy = destroy;
    list->head = NULL;
    list->tail = NULL;

    return;
}

/* dlist_destroy */
/* Complexity: O(n) */
void dlist_destroy(DList *list)
{
    void *data;

    /* Remove each element. */
    while (dlist_size(list) > 0)
    {
        if (dlist_remove(list, dlist_tail(list), (void **)&data) == 0 &&
            list->destroy != NULL)
        {
            /* Call a user-defined function to free dynamically allocated data.
             */
            list->destroy(data);
        }
    }

    /* No operations are allowed now, but clear the structure as a precaution.
     */
    memset(list, 0, sizeof(DList));

    return;
}

/* dlist_ins_next */
/* Complexity: O(1) */
int dlist_ins_next(DList *list, DListElmt *element, const void *data)
{
    DListElmt *new_element;

    /* Do not allow a NULL element unless the list is empty. */
    if (element == NULL && dlist_size(list) != 0)
        return -1;

    /* Allocate storage for the element. */
    if ((new_element = (DListElmt *)malloc(sizeof(DListElmt))) == NULL)
        return -1;

    /* Insert the new element into the list. */
    new_element->data = (void *)data;

    if (dlist_size(list) == 0)
    {
        /* Handle insertion when the list is empty. */
        list->head = new_element;
        list->head->prev = NULL;
        list->head->next = NULL;
        list->tail = new_element;
    }
    else
    {
        /* Handle insertion when the list is not empty. */
        new_element->next = element->next;
        new_element->prev = element;

        if (element->next == NULL)
            list->tail = new_element;
        else
            element->next->prev = new_element;

        element->next = new_element;
    }

    /* Adjust the size of the list to account for the inserted element. */
    list->size++;

    return 0;
}

/* dlist_ins_prev */
/* Complexity: O(1) */
int dlist_ins_prev(DList *list, DListElmt *element, const void *data)
{
    DListElmt *new_element;

    /* Do not allow a NULL element unless the list is empty. */
    if (element == NULL && dlist_size(list) != 0)
        return -1;

    /* Allocate storage to be managed by the abstract datatype. */
    if ((new_element = (DListElmt *)malloc(sizeof(DListElmt))) == NULL)
        return -1;

    /* Insert the new element into the list */
    new_element->data = (void *)data;

    if (dlist_size(list) == 0)
    {
        /* Handle insertion when the list is empty. */
        list->head = new_element;
        list->head->prev = NULL;
        list->head->next = NULL;
        list->tail = new_element;
    }
    else
    {
        /* Handle insertion when the list is not empty. */
        new_element->next = element;
        new_element->prev = element->prev;

        if (element->prev == NULL)
            list->head = new_element;
        else
            element->prev->next = new_element;

        element->prev = new_element;
    }

    /* Adjust the size of the list to account for the new element. */
    list->size++;

    return 0;
}

/* dlist_remove */
/* Complexity: O(1) */
int dlist_remove(DList *list, DListElmt *element, void **data)
{
    /* Do not allow a NULL element or removal from an empty list. */
    if (element == NULL || dlist_size(list) == 0)
        return -1;

    /* Remove the element from the list. */
    *data = element->data;

    if (element == list->head)
    {
        /* Handle removal from the head of the list. */
        list->head = element->next;

        if (list->head == NULL)
            list->tail = NULL;
        else
            element->next->prev = NULL;
    }
    else
    {
        /* Handle removal from other than the head of the list. */
        element->prev->next = element->next;

        if (element->next == NULL)
            list->tail = element->prev;
        else
            element->next->prev = element->prev;
    }

    /* Free the storage allocated by the abstract datatype. */
    free(element);

    /* Adjust the size of the list to account for the removed element. */
    list->size--;

    return 0;
}
```

## Description of Doubly-Linked Lists

### Doubly-Linked Lists

![Doubly-Linked Lists]({{site.baseurl}}/img/data-structures/doubly-linked-lists.jpg){:.inline-img-w800}

### dlist_ins_next()

#### Inserting an element into a doubly-linked list with dlist_ins_next()

1)
![dlist_ins_next_1]({{site.baseurl}}/img/data-structures/dlist_ins_next_1.jpg){:.inline-img-w800}

2)
![dlist_ins_next_2]({{site.baseurl}}/img/data-structures/dlist_ins_next_2.jpg){:.inline-img-w800}

3)
![dlist_ins_next_3]({{site.baseurl}}/img/data-structures/dlist_ins_next_3.jpg){:.inline-img-w800}

4)
![dlist_ins_next_4]({{site.baseurl}}/img/data-structures/dlist_ins_next_4.jpg){:.inline-img-w800}

#### Inserting an element into a doubly-linked list with dlist_ins_prev()

1)
![dlist_ins_prev_1]({{site.baseurl}}/img/data-structures/dlist_ins_prev_1.jpg){:.inline-img-w800}

2)
![dlist_ins_prev_2]({{site.baseurl}}/img/data-structures/dlist_ins_prev_2.jpg){:.inline-img-w800}

3)
![dlist_ins_prev_3]({{site.baseurl}}/img/data-structures/dlist_ins_prev_3.jpg){:.inline-img-w800}

4)
![dlist_ins_prev_4]({{site.baseurl}}/img/data-structures/dlist_ins_prev_4.jpg){:.inline-img-w800}

#### [!] Note

Remember to update the tail to point to the new tail when inserting an element
at the tail of the list.

### dlist_remove()

#### 1. Removing from the head of the list

1)
![dlist_remove_head_1]({{site.baseurl}}/img/data-structures/dlist_remove_head_1.jpg){:.inline-img-w800}
    
2)
![dlist_remove_head_2]({{site.baseurl}}/img/data-structures/dlist_remove_head_2.jpg){:.inline-img-w800}

#### 2. Removing from somewhere other than the head  

1)
![dlist_remove_elsewhere_1]({{site.baseurl}}/img/data-structures/dlist_remove_elsewhere_1.jpg){:.inline-img-w800}

2)
![dlist_remove_elsewhere_2]({{site.baseurl}}/img/data-structures/dlist_remove_elsewhere_2.jpg){:.inline-img-w800}

#### [!] Note

Remember to update the tail to point to the new tail when removing an element
at the tail of the list, or to NULL if removing an element has caused the list
to become empty.

Upon return, ???data??? points to the data stored in the element that was removed.
It is the responsibility of the caller to manage the storage associated with 
the data.
