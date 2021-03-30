---
layout: notes
title: "[Data Structures] Binary Trees"
meta: Implementation of Binary Trees
reference: Loudon, K. (1999). Mastering Algorithms with C. O'Reilly Media, Inc.
category: data-structures
---

## Header for the Binary Tree Abstract Datatype

```c
/* 
 * File Name    : bitree.h
 * Description  : Header for the Binary Tree Abstract Datatype
 * Reference    : Loudon, K. (1999). Mastering Algorithms with C. O'Reilly
 *                Media, Inc.
 */

#ifndef BITREE_H
#define BITREE_H

#include <stdlib.h>

/* Define a structure for binary tree nodes. */
typedef struct BiTreeNode_
{
    void                *data;
    struct BiTreeNode_  *left;
    struct BiTreeNode_  *right;
} BiTreeNode;

/* Define a structure for binary trees. */
typedef struct BiTree_
{
    int         size;
    int         (*compare)(const void *key1, const void *key2);
    void        (*destroy)(void *data);
    BiTreeNode  *root;
} BiTree;

/* Public Interface */
void bitree_init(BiTree *tree, void (*destroy)(void *data));
void bitree_destroy(BiTree *tree);
int bitree_ins_left(BiTree *tree, BiTreeNode *node, const void *data); 
int bitree_ins_right(BiTree *tree, BiTreeNode *node, const void *data); 
void bitree_rem_left(BiTree *tree, BiTreeNode *node);
void bitree_rem_right(BiTree *tree, BiTreeNode *node);
int bitree_merge(BiTree *tree, BiTree *left, BiTree *right, const void *data);
#define bitree_size(tree) ((tree)->size)
#define bitree_root(tree) ((tree)->root)
#define bitree_is_eob(node) ((node) == NULL)
#define bitree_is_leaf(node) ((node)->left == NULL && (node)->right == NULL)
#define bitree_data(node) ((node)->data)
#define bitree_left(node) ((node)->left)
#define bitree_right(node) ((node)->right)

#endif
```

## Implementation of the Binary Tree Abstract Datatype

```c
/* 
 * File Name    : bitree.c
 * Description  : Implementation of the Binary Tree Abstract Datatype
 * Reference    : Loudon, K. (1999). Mastering Algorithms with C. O'Reilly
 *                Media, Inc.
 */

#include <stdlib.h>
#include <string.h>

#include "bitree.h"

/* bitree_init */
/* Complexity: O(1) */
void bitree_init(BiTree *tree, void (*destroy)(void *data))
{
    /* Initialize the binary tree. */
    tree->size = 0;
    tree->destroy = destroy;
    tree->root = NULL;

    return;
}

/* bitree_destroy */
/* Complexity: O(n) */
void bitree_destroy(BiTree *tree)
{
    /* Remove all the nodes from the tree. */
    bitree_rem_left(tree, NULL);

    /* No operations are allowed now, but clear the structure as a precaution.
     */
    memset(tree, 0, sizeof(BiTree));

    return;
}

/* bitree_ins_left */
/* Complexity: O(1) */
int bitree_ins_left(BiTree *tree, BiTreeNode *node, const void *data)
{
    BiTreeNode  *new_node, **position;

    /* Determine where to insert the node. */
    if (node == NULL)
    {
        /* Allow insertion at the root only in an empty tree. */
        if (bitree_size(tree) > 0)
            return -1;

        position = &tree->root;
    }
    else
    {
        /* Normally allow insertion only at the end of a brench. */
        if (bitree_left(node) != NULL)
            return -1;

        position = &node->left;
    }

    /* Allocate storage for the node. */
    if ((new_node = (BiTreeNode *)malloc(sizeof(BiTreeNode))) == NULL)
        return -1;

    /* Insert the node into the tree. */
    new_node->data = (void *)data;
    new_node->left = NULL;
    new_node->right = NULL;
    *position = new_node;

    /* Adjust the size of the tree to account for the inserted node. */
    tree->size++;

    return 0;
}

/* bitree_ins_right */
/* Complexity: O(1) */
int bitree_ins_right(BiTree *tree, BiTreeNode *node, const void *data)
{
    BiTreeNode  *new_node, **position;

    /* Determine where to insert the node. */
    if (node == NULL)
    {
        /* Allow insertion at the root only in an empty tree. */
        if (bitree_size(tree) > 0)
            return -1;

        position = &tree->root;
    }
    else
    {
        /* Normally allow insertion only at the end of a branch. */
        if (bitree_right(node) != NULL)
            return -1;

        position = &node->right;
    }

    /* Allocate storage for the node. */
    if ((new_node = (BiTreeNode *)malloc(sizeof(BiTreeNode))) == NULL)
        return -1;

    /* Insert the node into the tree. */
    new_node->data = (void *)data;
    new_node->left = NULL;
    new_node->right = NULL;
    *position = new_node;

    /* Adjust the size of the tree to account for the inserted node. */
    tree->size++;

    return 0;
}

/* bitree_rem_left */
/* Complexity: O(n) */
void bitree_rem_left(BiTree *tree, BiTreeNode *node)
{
    BiTreeNode **position;

    /* Do not allow removal from an empty tree. */
    if (bitree_size(tree) == 0)
        return;

    /* Determine where to remove nodes. */
    if (node == NULL)
        position = &tree->root;
    else
        position = &node->left;

    /* Remove the nodes. */
    if (*position != NULL)
    {
        bitree_rem_left(tree, *position);
        bitree_rem_right(tree, *position);

        if (tree->destroy != NULL)
        {
            /* Call a user-defined function to free dynamically allocated data.
             */
            tree->destroy((*position)->data);
        }

        free(*position);
        *position = NULL;

        /* Adjust the size of the tree to account for the removed node. */
        tree->size--;

    }

    return;
}

/* bitree_rem_right */
/* Complexity: O(n) */
void bitree_rem_right(BiTree *tree, BiTreeNode *node)
{
    BiTreeNode **position;

    /* Do not allow removal from an empty tree. */
    if (bitree_size(tree) == 0)
        return;

    /* Determine where to remove nodes. */
    if (node == NULL)
        position = &tree->root;
    else
        position = &node->right;

    /* Remove the nodes */
    if (*position != NULL)
    {
        bitree_rem_left(tree, *position);
        bitree_rem_right(tree, *position);

        if (tree->destroy != NULL)
        {
            /* Call a user-defined function to free dynamically allcated data.
             */
            tree->destroy((*position)->data);
        }

        free(*position);
        *position = NULL;

        /* Adjust the size of the tree to account for the removed node. */
        tree->size--;
    }

    return;
}

/* bitree_merge */
/* Complexity: O(1) */
int bitree_merge(BiTree *merge, BiTree *left, BiTree *right, const void *data)
{
    /* Initialize the merged tree. */
    bitree_init(merge, left->destroy);

    /* Insert the data for the root node of the merge tree. */
    if (bitree_ins_left(merge, NULL, data) != 0)
    {
        bitree_destroy(merge);
        return -1;
    }

    /* Merge the two binary trees into a single binary tree. */
    bitree_root(merge)->left = bitree_root(left);
    bitree_root(merge)->right = bitree_root(right);

    /* Adjust the size of the new binary tree. */
    merge->size = merge->size + bitree_size(left) + bitree_size(right);

    /* Do not let the original trees access the merged nodes. */
    left->root = NULL;
    left->size = 0;
    right->root = NULL;
    right->size = 0;

    return 0;
}
```