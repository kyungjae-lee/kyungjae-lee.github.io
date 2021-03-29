---
layout: notes
title: "[Data Structures] Circular Lists"
meta: Implementation of Circular Lists
reference: Loudon, K. (1999). Mastering Algorithms with C. O'Reilly Media, Inc.
category: data-structures
---

## Header for the Circular List Abstract Datatype

```c
/* 
 * File Name    : clist.h
 * Description  : Header for the Linked List Abstract Datatype
 * Reference    : Loudon, K. (1999). Mastering Algorithms with C. O'Reilly
                  Media, Inc.
 */

#ifndef CLIST_H
#define CLIST_H

#include <stdlib.h>

/* Define a structure for circular list elements. */
typedef struct CListElmt_
{
    void                *data;
    struct CListElmt_   *next;
} CListElmt;

/* Define a structure for circular lists. */
typedef struct CList_
{
    int         size;
    int         (*match)(const void *key1, const void *key2);
    void        (*destroy)(void *data);
    CListElmt   *head;
} CList;

/* Public Interface */
void clist_init(CList *list, void (*destroy)(void *data));
void clist_destroy(CList *list);
int clist_ins_next(CList *list, CListElmt *element, const void *data);
int clist_rem_next(CList *list, CListElmt *element, void **data);
#define clist_size(list) ((list)->size)
#define clist_head(list) ((list)->head)
#define clist_data(element) ((element)->data)
#define clist_next(element) ((element)->next)

#endif
```

## Inplementation of the Circular List Abstract Datatype

```c
/* 
 * File Name    : clist.c
 * Description  : Inplementation of the Linked List Abstract Datatype
 * Reference    : Loudon, K. (1999). Mastering Algorithms with C. O'Reilly
 *                Media, Inc.
 */

#include <stdlib.h>
#include <string.h>

#include "clist.h"

/* clsit_init */
/* Complexity: O(1) */
void clist_init(CList *list, void (*destroy)(void *data))
{
    /* Initialize the list. */
    list->size = 0;
    list->destroy = destroy;
    list->head = NULL;

    return;
}

/* clist_destroy */
/* Complexity: O(n) */
void clist_destroy(CList *list)
{
    void *data;

    /* Remove each element. */
    while (clist_size(list) > 0)
    {
        if (clist_rem_next(list, list->head, (void **)&data) == 0 &&
            list->destroy != NULL)
        {
            /* Call a user-defined function to free dynamically allocated data.
             */
            list->destroy(data);
        }
    }

    /* No operations are allowed now, but clear the structure as a precaution.
     */
    memset(list, 0, sizeof(CList));

    return;
}

/* clist_ins_next */
/* Complexity: O(1) */
int clist_ins_next(CList *list, CListElmt *element, const void *data)
{
    CListElmt *new_element;

    /* Allocate storage for the element. */
    if ((new_element = (CListElmt *)malloc(sizeof(CListElmt))) == NULL)
        return -1;

    /* Insert the element into the list. */
    new_element->data = (void *)data;

    if (clist_size(list) == 0)
    {
        /* Handle insertion when the list is empty. */
        new_element->next = new_element;
        list->head = new_element;
    }
    else
    {
        /* Handle insertion when the list is not empty. */
        new_element->next = element->next;
        element->next = new_element;
    }

    /* Adjust the size of the list to account for the inserted element. */
    list->size++;

    return 0;
}

/* clist_rem_next */
/* Complexity: O(1) */
int clist_rem_next(CList *list, CListElmt *element, void **data)
{
    CListElmt *old_element;

    /* Do not allow removal from an empty list. */
    if (clist_size(list) == 0)
        return -1;

    /* Remove the element from the list. */
    *data = element->next->data;

    if (element->next == element)
    {
        /* Handle removing the last element. */
        old_element = element->next;
        list->head = NULL;
    }
    else
    {
        /* Handle removing other than the last element. */
        old_element = element->next;
        element->next = element->next->next;
        if (old_element == clist_head(list))
            list->head = old_element->next;
    }

    /* Free the storage allocated by the abstract datatype. */
    free(old_element);

    /* Adjust the size of the list to account for the removed element. */
    list->size--;

    return 0;
}
```