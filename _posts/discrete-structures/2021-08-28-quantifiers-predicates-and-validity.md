---
layout: notes
title: "[Discrete Structures] Quantifiers, Predicates, and Validity" 
meta: Quantifiers, predicates, validity
reference: 
category: discrete-structures
---

## Quantifiers and Predicates

A quantifier and its named variable are always placed in parentheses.

### Universal Quantifier (∀)

* Symbol - ∀ (an upside down A)
* Read "for all", "for every", "for each", or "for any"
* (∀x)P(x) is read "for all x, P(x) is true."
    - The first part is a *collection*, and the second part *describes* the
      colloection.
    - e.g., (∀x)(x > 0) is read "for all x, x > 0."

### Existential Quantifier (∃)

* Symbol - ∃ (a backward E)
* Read "there exists one", "for at least one", or "for some"
* (∃x)P(x) is read "there exists an x such that P(x) is true."
    - The first part is a *collection*, and the second part *describes* the
      colloection.
    - e.g., (∃x)(x > 0) is read "there exists an x such that x is greater than
      zero."

### Predicate (P(x))

* Expression - P(x)
* A property of the variable x.
    - Represents some unspecified predicate or property that *x* may have.
* Predicates involving properties of *n* variables are *n-ary* predicates.
    - P(x) - unary predicate
    - P(x,y) - binary prediate
    - P(x,y,z) - ternary predicate
    - ...

[!] Note: The symbol | is read "such that". 
* e.g., (∀x)|P(x) is exactly the same meaning as (∀x)P(x). 
It is read "for all x such that P(x) is true." 


## Interpretation

An **interpretation** for an expression involving predicates consists of the
following:

* A Collection of objects, called the **domain** of the interpretation, which
  must include at least one object
* An assignment of a property of the objects in the domain to each predicate
  in the expression
* An assignment of a particular object in the domain to each constant symbol
  in the expression


∃∀
