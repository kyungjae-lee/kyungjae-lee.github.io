---
layout: notes
title: "[Data Structures] Singly-Linked Lists"
meta: Implementation of Singly-Linked Lists
reference: Loudon, K. (1999). Mastering Algorithms with C. O'Reilly Media, Inc.
category: data-structures
---

## Header for the Linked List Abstract Data Type 

```c
/* 
 * File Name    : list.h
 * Description  : Header for the Linked List Abstract Datatype
 * Reference    : Loudon, K. (1999). Mastering Algorithms with C. O'Reilly
                  Media, Inc.
 */

#ifndef LIST_H
#define LIST_H

#include <stdlib.h>

/* Define a structure for linked list elements. */
typedef struct ListElmt_
{
    void                *data;
    struct ListElmt_    *next;
} ListElmt;

/* Define a structure for linked lists. */
typedef struct List_
{
    int         size;
    int         (*match)(const void *key1, const void *key2);
    void        (*destroy)(void *data);
    ListElmt    *head;
    ListElmt    *tail;
} List;

/* Public Interfaces */
void list_init(List *list, void (*destroy)(void *data));
void list_destroy(List *list);
int list_ins_next(List *list, ListElmt *element, const void *data);
int list_rem_next(List *list, ListElmt *element, void **data);
#define list_size(list) ((list)->size)
#define list_head(list) ((list)->head)
#define list_tail(list) ((list)->tail)
#define list_is_head(list, element) ((element) == (list)->head ? 1 : 0)
#define list_is_tail(element) ((element)->next == NULL ? 1 : 0)
#define list_data(element) ((element)->data)
#define list_next(element) ((element)->next)

#endif
```

## Implementation of the Linked List Abstract Datatype

```c
/* 
 * File Name    : list.c
 * Description  : Inplementation of the Linked List Abstract Datatype
 * Reference    : Loudon, K. (1999). Mastering Algorithms with C. O'Reilly
 *                Media, Inc.
 */

#include <stdlib.h>
#include <string.h>

#include "list.h"

/* list_init */
/* Complexity: O(1) */
void list_init(List *list, void (*destroy)(void *data))
{
    /* Initialize the list. */
    list->size = 0;
    list->destroy = destroy;
    list->head = NULL;
    list->tail = NULL;

    return;
}

/* list_destroy */
/* Complexity: O(n) */
void list_destroy(List *list)
{
    void *data;

    /* Remove each element. */
    while (list_size(list) > 0)
    {
        if (list_rem_next(list, NULL, (void **)&data) == 0 && list->destroy !=
            NULL)
        {
            /* Call a user-defined function to free dynamically allocated data.
             */
            list->destroy(data);
        }
    }

    /* No operations are allowed now, but clear the structure as a precaution.
     */
    memset(list, 0, sizeof(List));

    return;
}

/* list_ins_next */
/* Complexity: O(1) */
int list_ins_next(List *list, ListElmt *element, const void *data)
{
    ListElmt *new_element;

    /* Allocate storage for the element. */
    if ((new_element = (ListElmt *)malloc(sizeof(ListElmt))) == NULL)
        return -1;

    /* Insert the element into the list. */
    new_element->data = (void *)data;

    if (element == NULL)
    {
        /* Handle insertion at the head of the list. */
        if (list_size(list) == 0)
            list->tail = new_element;

        new_element->next = list->head;
        list->head = new_element;
    }
    else
    {
        /* Handle insertion somewhere other than at the head. */
        if (element->next == NULL)
            list->tail = new_element;

        new_element->next = element->next;
        element->next = new_element;
    }

    /* Adjust the size of the list to account for the inserted element. */
    list->size++;

    return 0;
}

/* list_rem_next */
/* Complexity: O(1) */
int list_rem_next(List *list, ListElmt *element, void **data)
{
    ListElmt *old_element;

    /* Do not allow removal from an empty list. */
    if (list_size(list) == 0)
        return -1;

    /* Remove the element from the list. */
    if (element == NULL)
    {
        /* Handle removal from the head of the list. */
        *data = list->head->data;
        old_element = list->head;
        list->head = list->head->next;

        if (list_size(list) == 1)
            list->tail = NULL;
    }
    else
    {
        /* Handle removal from somewhere other than the head. */
        if (element->next == NULL)
            return -1;

        *data = element->next->data;
        old_element = element->next;
        element->next = element->next->next;

        if (element->next == NULL)
            list->tail = element;
    }

    /* Free the storage allocated by the abstract datatype. */
    free(old_element);

    /* Adjust the size of the list to account for the removed element. */
    list->size--;

    return 0;
}
```
