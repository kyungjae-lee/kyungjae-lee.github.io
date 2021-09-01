---
layout: notes
title: "[Discrete Structures] Statements, Symbolic Representation, and
Tautologies" 
meta: Important facts about statements, symbolic representation, and tautologies
reference: 
category: discrete-structures
---

## Statement (or Proposition)

A statement (or proposition) is a declarative sentence that can be determined
or evaluated to be either true or false.

Followings are statements.
* Ten is less than seven. (False)
* Seoul is the capital of South Korea. (True)
* There are life forms on other planets in the universe. (Either true or false;
  we do not have to be able to decide which.)

Followings are NOT statements. Use this rule!
* The number X is positive. (X is not known)
* He is a baseball pitcher. (Do not know who 'he' is)
* Are you a Freshmen? (Questions are definitely not statements.)
    * You are a Freshmen. (If who 'you' is known, it is a statement.)
* Leave the room. (Command)


## Statement Letters

Uppercase/lower case letters such as A, B, C, p, q, r that are used to 
represent the statements.


## Logical Connectives

* Disjunction - A∨B (read "A or B")
    - A, B - disjuncts
* Conjunction - A∧B (read "A and B")
    - A, B - conjuncts
* Negation - A' (read "not A")
    - ~ or bar over the top of the object or propositional variable may be used
* Implication - if...then (→), A→B (read "A implies B")
    - A - hypothesis, antecedent, sufficient condition
    - B - conclusion, consequent, necessary condition
* Equivalence - if and only if (↔), A↔B stands for (A→B)∧(B→A) 

NOT(unary connective) needs only one statement whereas others(binary connectives)
must have at least two statements.

### Basic Truth Tables

![basic-truth-tables]({{site.baseurl}}/img/discrete-structures/basic-truth-tables.jpg){:.inline-img-w500}

### English Words and Logical Connectives

![english-words-and-logical-connectives]({{site.baseurl}}/img/discrete-structures/english-words-and-logical-connectives.jpg){:.inline-img-w700}

### Negation of a statement

![negation-of-a-statement]({{site.baseurl}}/img/discrete-structures/negation-of-a-statement.jpg){:.inline-img-w700}


## Well-Formed-Formula (WFF)

An expression that is legitimate.
* e.g., (A→B)∧(B→A) is a wff.
* e.g., A))∧∧→BC is not a wff.

In a wff with a number of connectives, the connective to be applied last is the
'main connective'.
* e.g., ((A∨B)∧C)→(B∨C')
    - main connective is '→'


## Order of Precedence of Connectives

1. connectives within parentheses, innermost parentheses first
2. '
3. ∧, ∨
4. →
5. ↔

If there are several logical connectives of the same precedence, they will be
examined left to right.

* e.g., A∨B∧B is equivalent to (A∨B)∧B

## Truth Table of Compound Statements

The total number of rows in a truth table for *n* statement letters is 2^*n*.

### Examples

![truth-table-of-compound-statements]({{site.baseurl}}/img/discrete-structures/truth-table-of-compound-statements.jpg){:.inline-img-w900}


## Tautologies

If the truth values of the main connective are,
* all T's - Tautology (don't need if statements in the end)
* all F's - Contradiction, Ausurdity (don't need if statements in the end)
* T's, F's - Contingency (evaluates to true or false depending on the
  individual component statements and still need if statements) 

### Some Tautological Equivalences

*Logical Equivalent* or *Equal* means 'have the same True Table'.

Each equivalence in a pair is called the *dual* of the other.
* In each pair, one equivalence can be obtained from the other by replacing 
∨ to ∧, ∧ to ∨, 1 to 0, 0 to 1.

![tautological-equivalence]({{site.baseurl}}/img/discrete-structures/tautological-equivalence.jpg){:.inline-img-w900}


## De Morgan's Laws

(A∨B)'↔A'∧B' and (A∧B)'↔A'∨B'

* AND(OR) to OR(AND), combined complement to separate
* Each is the dual of the other.
* Useful in expressing the negation of a compound statement
