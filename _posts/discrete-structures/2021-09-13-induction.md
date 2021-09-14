---
layout: notes
title: "[Discrete Structures] Induction"
meta: First principle of mathematical induction
reference: 
category: discrete-structures
---

## Examples

### Example 1

Prove that the equation

*1 + 2 + 3 + ... + n = n(n + 1)/2*

is true for every positive integer. Here the property *P(n)* is the equation.

**Proof by Mathematical Induction**

* Proceed by inudction on *n*, and let *S* be the set of positive integers for
which the statement *P(n)* is ture.
* STEP 1. Show *1 ∈ S* (Basis step).
    - *1 = 1(1 + 1)/2 = 2/2 = 1*
    - It follows *1 ∈ S*.
    - [!] Note: May not be *1* all the time. Start with the first element of
      the set *S*.
* STEP 2. Assume *k ∈ S* for an arbitrary *k ≥ 1*. So,
    - *1 + 2 + 3 + ... + k = k(k + 1)/2* 
        - Induction Hypothesis (IHOP) 
* STEP 3. Show *k + 1 ∈ S*. 
    - [!] Note: It must be shown that,
        - *1 + 2 + 3 + ... + k + (k + 1) = (k + 1)(k + 2)/2* 
    - Add *k + 1* to both sides of IHOP.
        - *1 + 2 + 3 + ... + k + (k + 1) = k(k + 1)/2 + (k + 1)* 
        - (left side) = *k(k + 1)/2 + 2(k + 1)/2*
        - (left side) = *(k + 1)(k + 2)/2*
    - Showing that *k + 1 ∈ S*.
* It follows by the Principle Mathematical Induction (PMI) that *S = N*; hence
  *P(n)* is true for every *n*.

### Example 2

Prove that the equation

*4 + 10 + 16 + ... + (6n - 2) = n(3n + 1)*

is true for every positive integer. Here the property *P(n)* is the equation.

**Proof by Mathematical Induction**

* Proceed by inudction on *n*, and let *S* be the set of positive integers for
which the statement *P(n)* is ture.
* STEP 1. Show *1 ∈ S* (Basis step).
    - *4 = 1(3 * 1 + 1) = 1(4) = 4*
    - Thus, *1 ∈ S*.
    - [!] Note: May not be *1* all the time. Start with the first element of
      the set *S*.
* STEP 2. Assume *k ∈ S* for an arbitrary *k ≥ 1* (or *k ∈ N*). So,
    - *4 + 10 + 16 + ... + (6n - 2) = n(3n + 1)*
        - Induction Hypothesis (IHOP) 
* STEP 3. Show *k + 1 ∈ S*. 
    - [!] Note: It must be shown that,
        - *4 + 10 + 16 + ... + (6k - 2) + (6(k + 1) - 2) = (k + 1)(3(k + 1) + 1)*
    - Add *k + 1* to both sides of IHOP.
        - *4 + 10 + 16 + ... + (6k - 2) + (6(k + 1) - 2) = k(3k + 1) + (6(k + 1) - 2)* 
        - (left side) = *3k^2 + k + 6k + 6 - 2*
        - (left side) = *3k^2 + 7k + 4*
        - (left side) = *3k^2 + 3k+ 4k + 4*
        - (left side) = *3k(k + 1)+ 4(k + 1)*
        - (left side) = *(k + 1)(3k + 4)*
        - (left side) = *(k + 1)(3k + 3 + 1)*
        - (left side) = *(k + 1)(3(k + 1) + 1)*
    - Showing that *k + 1 ∈ S*.
* It follows by the Principle Mathematical Induction (PMI) that *S = N*; hence
  *P(n)* is true for every *n*.



