---
layout: notes
title: "[Discrete Structures] Propositional Logic" 
meta: Valid argument, proof sequence, derivation rules for propositional logic,
    deduction method and other rules, verbal arguments
reference: 
category: discrete-structures
---

We want to use tools from formal logic to see how to reach logical conclusions
based on given statements (or propositions). The formal system that uses
propositional *wff* is called *propositional logic, statement logic, or
propositional calculus*.

[!] Note: *wff* stands for *well-formed-formula*


## Valid Arguments

An argument can be represented in symbolic form as

P1 ∧ P2 ∧ P3 ∧ ... ∧ Pn → Q 

* P's are the given statements, called the *hypotheses*, of the argument.
* Q is the *conclusion*.

Above propositional *wff* is called a **valid argument** when it is a 
tautology.

"Q logically follows from P1, P2, P3, ... , Pn."

[!] Note: This implication is true if any of the hypotheses is false, but in an
argument we usually care about what happens when all the hypotheses are true.


## Proof Sequence

A sequence of *wff*s in which each *wff* is either a hypothesis or the result 
of applying one of the formal system's derivation rules to earlier *wff*s in 
the sequence.

|P1     |(hypothesis)                                               |              
|P2     |(hypothesis)                                               |
|...    |...                                                        |
|Pn     |(hypothesis)                                               |
|wff1   |(obtained by applying a derivation rule to earlier *wff*)  |
|...    |...                                                        |
|Q      |(obtained by applying a derivation rule to earlier *wff*)  |

### Example

(P → Q) ∧ (Q → R) → (P → R)

|1. P → Q   | hypothesis                        |
|2. Q → R   | hypothesis                        |
|3. P       | hypothesis, or deduction method   |
|4. Q       | modus ponens, 1, 3                |
|5. R       | modus ponens, 2, 4                |



## Derivation Rules for Propositional Logic

Derivation rules for propositional logic fall into two categories:
* Equivalence rules
* Inference rules

### Equivalence Rules

Equivalence rules are truth-preserving; a true *wff* remains true if a
substitution is done within it.

[!] Note: Equivalence rules work in both directions! (Expressions are 
equivalent to each other. They have exactly the same truth tables.)

![equivalence-rules]({{site.baseurl}}/img/discrete-structures/equivalence-rules.jpg){:.inline-img-w700}

### Inference Rules

Inference rules say that if one or more *wff*s that match the first part of the
rule pattern are already part of the proof sequence, we can add to the proof
sequence a new *wff* that matches the last part of the rule pattern. 

Inference rules are also truth-preserving.

[!] Note: Inference rules work in only one direction!

![inference-rules]({{site.baseurl}}/img/discrete-structures/inference-rules.jpg){:.inline-img-w700}

![more-inference-rules]({{site.baseurl}}/img/discrete-structures/more-inference-rules.jpg){:.inline-img-w700}

### Derivation Hints

![derivation-hints]({{site.baseurl}}/img/discrete-structures/derivation-hints.jpg){:.inline-img-w700}


## Deduction Method and Other Rules

### Deduction Method

P1 ∧ P2 ∧ P3 ∧ ... ∧ Pn → (R → S) 

Can be rewritten as, 

P1 ∧ P2 ∧ P3 ∧ ... ∧ Pn ∧ R → S 

by **Deduction method**.

### Hypothetical Syllogism

From *P → Q* and *Q → R*, one can derive *P → R*.

*Hypothetical syllogism* makes the following a valid argument.

(P → Q) ∧ (Q → R) → (P → R)

[!] Note: See the example in the *Proof Sequence* section for the proof
sequence of this argument.


## Verbal Arguments

An argument in English can be tested for validity by a two-step process:

1. Symbolize the argument using propositional *wff*s.
2. Prove that the argument is valid by constructing a proof sequence for it
   using the derivation rules for propositional logic.

### Example

Is the following argument valid?

"My client is left-handed, but if the diary is not missing, then my client is
not left-handed; therefore, the diary is missing."

* L - My client is left-handed.
* D - The diary is missing.

The argument is then

L ∧ (D' → L') → D

The validity of the argument is established by the following proof sequence.

|1. L           | hypothesis                        |
|2. D' → L'     | hypothesis                        |
|3. (D')' ∨ L'  | implication, 2                    |
|4. D ∨ L'      | double negation, 3                |
|5. L' ∨ D      | commutative, 4                    |
|6. L → D       | implication, 5                    |
|7. D           | implication, 1, 6                 |
