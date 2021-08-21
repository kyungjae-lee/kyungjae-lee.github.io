---
layout: notes
title: "[C Programming] Combination of const Keyword and Pointers"
meta: Combination of const keyword and pointers, and their meanings
reference: 
category: c-programming
---


## Constant Pointers

A constant pointer is a pointer that cannot change the address its holding. In
other words, once a constant pointer points to a variable then it cannot point
to any other variable.

## Pointer to Constant

A pointer through which one cannot change the value of variable it points.
These type of pointers can change the address they point to but cannot change
the value kept at those address.

## Examples

```c
int *ptr;               // ptr: a pointer to an int

const int *ptr;         // ptr: a pointer to a const int 
                        // value of variable CANNOT get changed through ptr
                        // ptr CAN point to a different variable

int * const ptr;        // ptr: a const pointer to an int
                        // value of variable CAN get changed through ptr
                        // ptr CANNOT point to a different variable

const int * const ptr;  // ptr: a const pointer to a const int
                        // value of variable CANNOT get changed through ptr
                        // ptr CANNOT point to a different variable
```

The first 'const' can be on either side of the type.

```c
const int *ptr;         /* is identical to */ int const *ptr;
const int * const ptr   /* is identical to */ int const * const ptr;
```

## More Examples

```c
int **ptr;              // ptr: a pointer to a pointer to an int
int ** const ptr;       // ptr: a const pointer to a pointer to an int
int * const *ptr;       // ptr: a pointer to a const pointer to an int
const int **ptr;        // ptr: a pointer to a pointer to a const int    
int * const * const ptr;// ptr: a const pointer to a const pointer to an int
```

