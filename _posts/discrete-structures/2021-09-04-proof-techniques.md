---
layout: notes
title: "[Discrete Structures] Proof Techniques" 
meta: Counterexample, exhaustive proof, direct proof, contraposition,
    contradiction, serendipity
reference: 
category: discrete-structures
---

## Proof Techniques

**Proof**
* An impeccable argument.
* Use only methods of pure logic.
* Infers the validity of a given mathematical assertion.

**Axiom**
* A Proposition regarded as self-evidently true without proof.

**Inductive Reasoning**
* Inductive reasoning draws a conclusion based on experience.
    - e.g., For the conjecture P → Q, the more cases you find where Q follows
      from P, the more confident you are in your conjecture.
    - No matter how reasonable the conjecture sounds, however, you will not be
      satisfied until you have applied *deductive reasoning* as well.

**Deductive Reasoning**
* Deductive reasoning starts out with a general statement, or hypothesis, and
  examines the possibilities to reach a specific, logical conclusion.

### 1. Counterexample

* Counterexample of a conjecture P → Q is a case in which P is true but Q is 
false. 
* One counterexample is enough to disprove a conjecture.
    - Find one example that the proposition does not hold true, then it is
      generally not true.
* If a counterexample is not forthcoming, perhaps the conjecture is true and we
should try to prove it!
* e.g., If *x* and *y* are integers and *x^2 = y^2*, then  *x = y*.
    - *x = 2, y = -2* (Just find one example.)

### 2. Exhaustive Proof

* Exhaustive proof proving the conjecture true by showing that it is true for
every member of the collection. (The persone doing the proof is exhausted as
well!)
* e.g., Prove the conjecture, "*n! <= n^2, for 0 < n <= 3.* (*n* is natural
  number)" 
    - When n = 1, 1! <= 1^2, 1 <= 1, true!
    - When n = 2, 2! <= 2^2, 2 <= 4, true!
    - When n = 3, 3! <= 3^2, 6 <= 9, true!
* [i] Note: Divides
    - *a* divides *b* (*a*\|*b*) iff there is an integer d such that *ad = b*.
    - e.g., All integers divide zero. *a*\|*0* iff there is an integre d such
      that *ad = 0*. (When *d = 0*, this is true.)

### 3. Direct Proof (Modus Ponens)

* Direct proof assumes the hypothesis and deduces the conclusion.
* e.g., If *x^3 - x^2 + x - 1 = 0*, then *x = 1* where *x ∈ R*.
    - *(x - 1)(x^2 + 1) = 0*
    - *x = 1* or *x^2 + 1 = 0*
    - *x^2 + 1 = 0* can't happen, so *x = 1* 

### 4. Contraposition


### 5. Contradiction

### 6. Serendipity
