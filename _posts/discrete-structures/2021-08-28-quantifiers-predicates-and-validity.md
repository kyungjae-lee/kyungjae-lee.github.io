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


## Scope and Free Variable

"Grouping symbols" such as parentheses and brackets identify the **scope** of a
quantifier, the section of the *wff* to which the quantifier applies.
* e.g., (∀x)[(∃y)[P(x, y) ∧ Q(x, y)] → R(z)]
    - Scope of x - (∃y)[P(x, y) ∧ Q(x, y)] → R(z)
    - Scope of y - P(x, y) ∧ Q(x, y)

**Free variable** is a variable occurs somewhere in a *wff* where it is NOT
part of a quantifier and is NOT within the scope of a quantifier involving
that variable. 
* e.g., (∀x)[(∃y)[P(x, y) ∧ Q(x, y)] → R(z)]
    - Free variable - z (not part of the given quantifiers)
* e.g., (∀x)[P(x) ∧ Q(x)] → R(x)
    - Free variable - x of R(x) (not within the scope of the given quantifier)
    - [!] Note: Don't be fooled by the variable's appearance!

 
## Translation

P(x) = x is a parrot, U(x) = x is ugly

* (∀x)[P(x) → U(x)]
    - For everything in the world, if it is a parrot, it is ugly.
    - For everything which is a parrot, it is ugly.
    - Every parrot is ugly.
* (∃x)[P(x) ∧ U(x)]
    - There is at least one thing that is both a parrot and ugly.
    - There is an ugly parrot.

Think each of (∀ →), and (∃ ∧) is a good combination.

[!] Note: the *wff* (∀x)[P(x) ∧ U(x)] is an incorrect translation because it
says that everything in the domain - understood here to be the whole world - is
an ugly parrot. This says something much stronger than the original English
statement.

[!] Note: the *wff* (∃x)[P(x) → U(x)] is an incorrect translation because it is
true as long as there is anything, call it x, in the domain (the whole world)
that is not a parrot, because then P(x) is false and the implication is true.
(Indeed, this *wff* is true if there are no parrots in the world at all!)
