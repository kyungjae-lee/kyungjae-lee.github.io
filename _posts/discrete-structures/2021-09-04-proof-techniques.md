---
layout: notes
title: "[Discrete Structures] Proof Techniques" 
meta: Counterexample, exhaustive proof, direct proof, contraposition,
    contradiction, serendipity
reference: 
category: discrete-structures
---

## Proof Techniques

* **Proof**
    - An impeccable argument.
    - Use only methods of pure logic.
    - Infers the validity of a given mathematical assertion.
* **Axiom**
    - A Proposition regarded as self-evidently true without proof.
* **Inductive Reasoning**
    - Inductive reasoning draws a conclusion based on experience.
        - e.g., For the conjecture P → Q, the more cases you find where Q 
          follows from P, the more confident you are in your conjecture.
        - No matter how reasonable the conjecture sounds, however, you will not
          be satisfied until you have applied *deductive reasoning* as well.
* **Deductive Reasoning** 
    - Deductive reasoning starts out with a general statement, or hypothesis, 
      and examines the possibilities to reach a specific, logical conclusion.


[!] Note: "If and only if" requires two proofs, one in each direction.

[!] Note: To prove that something is not ture, try proof by contradiction.

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

### 4. Contraposition (Indirect Proof)

* Contraposition is the technique of proving P → Q by doing a direct proof of 
Q' → P'.
    - Making use of (P → Q) ↔ (Q' → P') 
    - [!] Note: (Q' → P') → (P → Q) is a tautology.
    - [!] Note: Q' → P' is called the *contrapositive* of P → Q.
* e.g., If *x^3 - x^2 + x - 1 = 0*, then *x = 1* where *x ∈ R*.
    - Contrapositive of this is if *(x = 1)*', then *(x^3 - x^2 + x - 1 = 0)*'.
    - If *x ≠ 1*, then *x^3 - x^2 + x - 1 ≠ 0*.
    - If *x ≠ 1*, then *(x^2 + 1)(x - 1) ≠ 0*.
    - If *x ≠ 1*, then *x - 1 ≠ 0*, then *(x^2 + 1)(x - 1) ≠ 0*.
    - So, now, by contrapositive, if *x^3 - x^2 + x - 1 = 0*, then *x = 1*.
        - This final statement is very important! Do not miss it!
* [!] Note: Errors in proof by *contraposition*
    - P' → Q' (negate but not reverse) A.K.A **inverse**
        - P → Q and P' → Q' are not equivalent.
        - Proving P' → Q' does not prove P → Q.
    - Q → P (reverse but not negate) A.K.A **converse**
        - P → Q and Q → P are not equivalent.
        - Proving Q → P does not prove P → Q.
        - e.g., Original: If *a > 5*, then *a > 2*. (True) / Converse: If *a > 2*, then *a > 5*. (False)


### 5. Contradiction (Indirect Proof)

* *Reductio ad adsurdum*
* Make an assumption and show that leads to the contradiction.
* When trying to prove P → Q, by constructing a truth table, it's obtained that
(P ∧ Q' → 0) → (P → Q) is a tautology. So to prove the theorem P → Q, it is
sufficient to prove P ∧ Q' → 0.
    - Therefore, in a proof by contradiction you assume that both the
      hypothesis and the negation of the conclusion are true and then ry to
      deduce some contradiction from these assumptions.
* e.g., If *x^3 - x^2 + x - 1 = 0*, then *x = 1* where *x ∈ R*.
    - We are given '*x^3 - x^2 + x - 1 = 0*' and we know this is true. We'll
      assume *x ≠ 1*. 
    - Assume *x^3 - x^2 + x - 1 = 0* and *x ≠ 1*. Then *x - 1 ≠ 0*.
    - But, *x^3 - x^2 + x - 1 = (x - 1)(x^2 + 1) = 0*.
    - So, since *x ≠ 1*, then *x^2 + 1 = 0*, which is impossible in *x ∈ R*.
    - ∴ (therefore) *x = 1*.
* [!] Note: Errors in proof by *contradiction*
    - Inadvertent direct proof
        - Goal: prove P → Q
        - Mistake: assume P ∧ Q', deduce Q (rather than contradiction) witout
          using Q'
        - Incorrectly claim Q ∧ Q' as contradiction  
        - Actually direct proof P → Q
    - Inadvertent proof by contraposition
        - Mistake: assume P ∧ Q', deduce P' (rather than contradiction) witout
          using P 
        - Incorrectly claim P ∧ P' as contradiction  
        - Actually direct proof of Q' → P', proof by contraposition of P → Q

### 6. Serendipity

* Proof by good luck!


## Proof Techniques Summary

![proof-technique-summary]({{site.baseurl}}/img/discrete-structures/proof-technique-summary.jpg){:.inline-img-w700}