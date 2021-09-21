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
* [!] Note: If and only if (*iff*) proofs
    - Theorems may have form *P* if and only if *Q*.
        - "if and only if" AKA "*iff*"
    - Parts of "if and only if"
        - *P* if *Q* means *Q → P*
        - *P* only if *Q* means *P → Q*
    - To prove *P iff Q*, prove **both** P → Q and Q → P.
        - Not a separate proof technique
        - If and only if requires two proofs
        - Parts of proof may use same or different techniques
* e.g., If *x^3 - x^2 + x - 1 = 0*, then *x = 1* where *x ∈ R*.
    - *(x - 1)(x^2 + 1) = 0*
    - *x = 1* or *x^2 + 1 = 0*
    - *x^2 + 1 = 0* can't happen, so *x = 1* 
* e.g., *x*\|*y* (*x* divides *y*, *y* is divisible by *x*) if and only if there
  is an integer *n* (*n ∈ Z*) such that *y = xn*.
    - Theorem. If *n*\|*m* and *m*\|*p* then *n*\|*p*.
    - Proof.
        - Let *n*\|*m*, then there is an integer *a* such that *m = an*.
        - Let *m*\|*p*, then there is an integer *b* such that *p = bm*.
        - Substitute for *m* in *p = bm*, to give *p = bm = b(an) = (ab)n.*
        - Therefore *n*\|*p*. 
* e.g., Given any consecutive integers, one of them is odd, one of them is
  even.
    - Restatement. If *m* and *n* are consecutive integers, then either *m* is
      even *n* is odd, or vice versa.
        - [!] Note: As we cannot assume *m* to be odd (or even), we need to
          prove both cases.
    - Proof.
        - Case 1. Assume *m* is even, the smaller of *m* and *n*. Then ∃k, 
          *k ∈ Z* where *m = 2k*. So, *m + 1 = n = 2k + 1* which is odd.
        - Case 2. Assume *m* is odd, the smaller of *m* and *n*. Then ∃k, 
          *k ∈ Z* where *m = 2k + 1*. So, *m + 1 = n = (2k + 1) + 1 = 2(k + 1)*
          which is even.
* e.g., Given integers *x* and *y*, product *xy* is odd if and only if *x* and
  *y* are odd integers.
    - Proof.
        - Case 1. If *x* and *y* are odd integers, then *xy* is odd.
        - Suppose *x* and *y* are odd.
        - Then, *x = 2n + 1* and *y = 2m + 1*, where *m* and *n* are integers.
            - [!] Note: In general, *x* and *y* can be the same or different.
              We do not know! Make sure to use different character(e.g., m, n)
              to express *x* and *y*.
        - Then, *xy = (2n +1)(2m + 1) = 4mn + 2m + 2n + 1 = 2(2mn + m + n) + 1*.
        - This has the form *2k + 1*, where *k = (2nm + 2m  + n)* is an
          integer, so *xy* is odd.
        - Case 2. If *xy* is odd then *x* and *y* are odd integers. 
            - [!] Note: It is very though to do direct proof so let's use
              contrapositive.
        - Contrapositive. If **NOT**(*x* and *y* are odd), then **NOT**(*xy* is
          odd).
        - If *x* or *y* are not odd, then *xy* is not odd.
        - If *x* is even or *y* is even, then *xy* even.
        - The antecedent has three cases:
            1. *x* even, *y* odd: *x = 2m, y = 2n + 1. Then, *xy* = (2m)(2n +
               1) = 2(2mn + m), which is even.
            2. *x* odd, *y* even: *x = 2m + 1, y = 2n. Then, *xy* = 
               (2m + 1)(2n) = 2(2mn + m), which is even.
            3. *x* even, *y* even: *x = 2m, y = 2n. Then, *xy* = (2m)(2n)
               = 2(2mn), which is even.
        - Thus, (*xy* odd) → (*x* and *y* are odd) by contraposition.

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
* e.g., If the square of an integer is odd, then the integer is odd.
    - Restatement. If *n^2* is odd, then *n* is odd, where *n ∈ Z*.
    - Contrapositive. If *n* is **NOT** odd, then *n^2* is **NOT** odd, where
      *n ∈ Z*.
    - If *n* is even, then *n^2* is even. ∃k, *k ∈ Z* where *n = 2k*.
    - So, *n^2 = (2k)^2 = 4k^2 = 2(2k^2)*.
    - Therefore *n^2* is even.
        - [!] Note: This is NOT the end!
    - Thus, if *n^2* is odd, then *n* is odd, where *n ∈ Z*.
        - [!] Note: Finish with the original statement.
* [!] Note: Errors in proof by *contraposition*
    - P' → Q' (negate but not reverse) A.K.A **inverse**
        - P → Q and P' → Q' are not equivalent.
        - Proving P' → Q' does not prove P → Q.
    - Q → P (reverse but not negate) A.K.A **converse**
        - P → Q and Q → P are not equivalent.
        - Proving Q → P does not prove P → Q.
        - e.g., Original: If *a > 5*, then *a > 2*. (True) / 
          Converse: If *a > 2*, then *a > 5*. (False)


### 5. Contradiction (Indirect Proof)

* *Reductio ad adsurdum*
* Make an assumption and show that leads to the contradiction.
* When trying to prove P → Q, by constructing a truth table, it's obtained that
(P ∧ Q' → 0) → (P → Q) is a tautology. So to prove the theorem P → Q, it is
sufficient to prove P ∧ Q' → 0.
    - Therefore, in a proof by contradiction you assume that both the
      hypothesis and the negation of the conclusion are true and then try to
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
