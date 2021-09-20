---
layout: notes
title: "[Discrete Structures] Recursion Definitions"
meta: Recursively defined sequences, recursively defined sets, recursively
    defined operations
reference: 
category: discrete-structures
---

A definition in which the item being defined appears as part of the definition
is called a **recursive definition**.

Recursive (or inductive) definition consists of two parts:
1. A basis step
    - Where some simple cases of the item being defined are explicitly given
    - Gives us a place to start
2. An inductive or recursive step
    - Where new cases of the item being defined are given in terms of previous
      cases


## Recursively Defined Sequences

A **sequence** is a collection of objects in which order is important.

A sequence *S* (an infinite sequence) is defined recursively by:
1. Defining the first (or first few) objects explicitly
2. Defining later objects in terms of early ones

* e.g., The sequence *S* is defined recursively by:
1. *S(1) = 2*
2. *S(n) = 2S(n - 1) for n ≥ 2*
    - e.g., *S(4)* = *2S(3)* = *2(2S(2))* = *2(2(2S(1)))* = 2(2(2·2) = 2(2(4))
      = 2(8) = 16

* e.g., The **Fibonacci sequence** is defined recursively by:
1. *F(1) = 1, F(2) = 1*
2. *F(n) = F(n -2) + F(n - 1) for n > 2*
    - e.g., *F(3) = F(2) + F(1) = 1 + 1 = 2*
    - e.g., *F(4) = F(3) + F(2) = 2 + 1 = 3*
    - e.g., *F(5) = F(4) + F(3) = 3 + 2 = 5*
    - e.g., Likewise, *F(6) = 5 + 3 = 8*, *F(7) = 8 + 5 = 13*, so on.
* e.g., Prove that in the Fibonacci sequence, *F(n + 4) = 3F(n + 2) - F(n) for
  all n ≥ 1*
    - *F(n + 4) = F(n + 3) + F(n + 2)*
    - *= F(n + 2) + F(n + 1) + F(n + 2)*
    - *= 2F(n +2) + F(n + 1)*
    - Since *F(n + 2) = F(n + 1) + F(n)*, *F(n + 1) = F(n + 2) - F(n)*
    - *= 2F(n +2) + F(n + 2) - F(n)*
    - *= 3F(n +2) - F(n)*


## Recursively Defined Sets

A **set** is a colloection of objects in which order is **NOT** important.
* Redundant elements are dropped.
* Typically uppercase letters are used to represent sets, and basically
  anything can be the elements of the sets.
* e.g., *S = { k, s, p } = { p, s, k }, k ∈ S* (the element *k* is part of the
  set *S*), *s ∈ S, p ∈ S*

A finite set (limit to the number of elements) is called an **alphabet**. 

A sequence of symbols from alphabet is called a **string**. (Mathematical
definition of string)

* e.g., The set of all (finite-length) strings of symbols over a finite
  alphabet *A* is denoted by *A\**. The recursive definition of *A\** is
  1. The **empty string λ** (the string with no symbols) belongs to *A\**.
     (Basis step)
  2. Any single member of *A* belongs to *A\**. (Basis step)
  3. If *x* and *y* are strings in *A\**, so is *xy*, the **concatenation** of
     strings *x* and *y*. (Recursive step)
    - e.g., If *x = 1011* and *y = 0101*, then *xy = 10110101* and 
      *yxy = 010111010101*

* e.g., **Bakus-Naur form (BNF)**. The syntax for programming languages are 
  defined by *BNF*.
    - Items in < > are defined in terms of other items and may be recursive.
    - Items not in brackets are not further defined. (**Terminals**)
    - Vertical bard (\|) denotes choice. Like an *or*. 
    - \<identifier> ::= \<letter> \| \<identifier>\<letter> \| 
      \<identifier\>\<digit\>
    - \<letter> ::= a \| b \| c \| ... \| z
    - \<digit> ::= 1 \| 2 \| 3 \| ... \| 9
    - \<number> ::= \<digit> \| \<number>\<digit> \| \<number>.(decimal point)
        - e.g., Thus the identiier *ch2* is built from the definition by a
          sequence of choices such as
          - \<identifier> can be \<identifier>\<digit>
          - which can be \<identifier>*2*
          - which can be \<identifier>\<letter>*2*
          - which can be \<identifier>*h2*
          - which can be \<letter>*h2*
          - which can be *ch2*

### Structural Induction

A form of induction connecting recursion and induction. This is another
technique that is specific to recursively defined sets.

Proof method for structural induction:
* Given recursively defined set *S* and property *P(x)* for *x ∈ S*, if these
  two conditions are true:
  1. *P(x)* is true for all elements *x ∈ S* defined in the basis. (Basis step)
  2. (*P(x)* for *x ∈ S*) → *P(y)* for *y ∈ S* where *y* is constructed from
     *x* using the recursive step (inductive step).
* Then *P(x)* is true for every *x ∈ S*.

e.g., A set *S* is defined recursively by:
1. The **empty string λ** (the string with no symbols) belongs to *S*.
2. If *x* belongs to *S*, so do *1x0* and *0x1*.

Given the above definition of *S* prove if *s ∈ S*, then *s* contains an equal
number of *0*s and *1*s.

Proof by structural induction
* Basis - The empty string λ has zero *0*s and zero *1*s.
* Inductive hypothesis - Show that any string *y* constructed from *x* has an
  equal number of *0*s and *1*s.
* [!] Note: There are two cases to consider from the recursive definition.
    - Case 1: *y = 1x0*. Then *y* will always have *k + 1* *1*s and *k + 1*
      *0*s.
    - Case 2: *y = 0x1*. Then *y* will always have *k + 1* *0*s and *k + 1*
      *1*s.
* Therefore, every string *s ∈ S* has an equal number of *0*s and *1*s.


## Recursively Defined WWFs (Well-Formed-Formula)

A **WWF** is defined recursively by:
1. Any statement letter is a *wff* (Basis step)
    - e.g., *a, b, c, Z, Y, X*
2. If *P* and *Q* are *wff*s, so are
    - *P ∧ Q*
    - *P ∨ Q*
    - *P → Q*
    - *P'*
    - *P ↔ Q*

[!] Note: Start from the single letter (basis step), if you can express the
given formula only by applying one of those 5 mentioned above, then it is
*wff*.
* e.g., Prove that ((A ∨ B') → C) is a *wff*.
    - *A, B, C* are *wff*s by rule 1.
    - By rule 2, *B'* is a *wff*.
    - And so then is *(A ∨ B')* is *(A ∨ B') → C*.


## Recursively Defined Operations    

Certain operations performed on objects can be defined recursively.

* e.g., A recursive definition of the exponentiataion operation *a^n* on a
  nonzero real number *a*, where *n* is a nonnegative integers, is
  1. *a^0 = 1*
  2. *a^n = (a^(n-1))a* for *n ≥ 1*

* e.g., A recursive definition for multiplication of two positive integers *m*
  and *n* is
  1. *m(1) = m*
  2. *m(n) = m(n - 1) + m* for *n ≥ 2*
