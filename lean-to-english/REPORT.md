# LLM Performance in Translating Lean Proofs to Natural Language

A small side experiment evaluating how well frontier Large Language Models can understand and explain formal proofs written in Lean 4.

## Methodology

**Models Tested:** ChatGPT 5.1 (Thinking, Extended) and Gemini 3 Pro  
**Test Materials:** 5 Lean files from the [leanprover-community/tutorials4](https://github.com/leanprover-community/tutorials4) repository  
**Preprocessing:** Comments were removed from all files for better testing of the models' abilities

### Prompt Used

> This is a lean file. Your task is:  
> 1) Find out what are the theorems in this file and explain them.  
> 2) Explain what the file is actually proving and how.

### Files Evaluated

| File | Topic |
|------|-------|
| `00FirstProofs.lean` | Upper/lower bounds, limits, infimum characterization |
| `01EqualityRewriting.lean` | `rw`, `calc`, and `ring` tactics for equalities |
| `02IffIfAnd.lean` | Logical equivalences, `linarith`, forward/backward reasoning |
| `03ForallOr.lean` | Universal quantifiers, function parity/monotonicity |
| `04Exists.lean` | Existential proofs, divisibility, surjectivity |

---

## Summary

**ChatGPT** used a more rigorous and math-heavy approach with detailed answers while **Gemini** leaned towards a code-focused and brief approach to explain the theorems and proofs. 

Both models **successfully** tackled the problems they were given which suggests that current frontier models have the ability to **understand and translate foundational level mathematical proofs** constructed in Lean. 

**00FirstProofs.lean**   
**([https://github.com/leanprover-community/tutorials4/blob/master/Tutorials/Solutions/00FirstProofs.lean](https://github.com/leanprover-community/tutorials4/blob/master/Tutorials/Solutions/00FirstProofs.lean))**  
   
This file contains definitions and theorems related to **real analysis**, specifically concerning **upper bounds, maximums, lower bounds, infimums (greatest lower bounds), and limits of sequences of real numbers**.

| Theorem / Concept | Explanation (Based on File) | ChatGPT 5.1  | Gemini 3 |
| :---- | :---- | :---- | :---- |
| **unique\_max** | **Uniqueness of Maximum:** Proves that if a set of real numbers has a maximum, it is unique . | **Yes.** Correctly noted that if two maxima exist, they must be equal due to antisymmetry. | **Yes.** Correctly stated that if a set has a maximum, it is unique. |
| **inf\_lt** | **"No Gap" Property:** If x is the infimum, any number y \> x is strictly greater than some element in the set. | **Yes.** Described as the "no gap" property; you cannot have a gap above the infimum without points. | **Yes.** Correctly explained via contraposition: if not, y would be a lower bound \> x. |
| **le\_of\_le\_add\_eps** | **Epsilon Trick:** If y \<= x \+ epsilon for all positive epsilon, then y \<= x . | **Yes.** Identified as the "classic epsilon trick" and noted the specific epsilon used in the proof.  | **Yes.** Correctly identified the statement and the contradiction proof structure. |
| **le\_lim** | **Limits Preserve Inequalities:** If u\_n to x and y \<=  u\_n for all n, then y \<= x . | **Yes.** Stated that a limit is "at least as large as any lower bound" for the sequence.  | **Yes.** Correctly explained that y is bounded by x because it is bounded by the sequence terms.  |
| **inv\_succ\_pos** | **Positivity:** For any natural number n, the real number 1/(n+1) is positive . | **Yes.** Correctly identified as a "small auxiliary lemma" for positivity.  | **Yes.** Correctly identified that the fraction is strictly positive.  |
| **limit\_inv\_succ** | **Convergence to 0:** The sequence 1/(n+1) eventually becomes smaller than any \\epsilon \> 0 . | **Yes.** Stated clearly as "The sequence 1/(n+1) tends to 0"  | **Yes.** Stated that the sequence converges to 0 using the Archimedean property  |
| **inf\_seq** | **Main Theorem:** Characterizes the infimum: x is the infimum iff it is a lower bound and is the limit of a sequence in the set . | **Yes.** Detailed the "two directions" of the proof (constructing the sequence vs. proving the bound)  | **Yes.** Identified as the "main result," linking the greatest lower bound to sequential limits  |
| **Overall Goal** | **Purpose:** To characterize infima of sets of real numbers in terms of sequences . | **Yes.** "Build machinery... to prove that every infimum is the limit of a sequence from the set" | **Yes.** “builds the necessary scaffolding …. to.. definition of an infimum with its topological sequential definition." |

[https://chatgpt.com/share/693809f5-e81c-8012-9ce9-68dd5845c4b0](https://chatgpt.com/share/693809f5-e81c-8012-9ce9-68dd5845c4b0)

[https://gemini.google.com/share/2e24dc11586d](https://gemini.google.com/share/2e24dc11586d)

**01EqualityRewriting.lean**

**([https://github.com/leanprover-community/tutorials4/blob/master/Tutorials/Solutions/01EqualityRewriting.lean](https://github.com/leanprover-community/tutorials4/blob/master/Tutorials/Solutions/01EqualityRewriting.lean))**

This file contains **exercises and explanations focused on using the rw and ring tactics for proving equalities of real numbers through algebraic calculation and symbolic manipulation.**

| Theorem / Concept | Explanation (Based on File) | ChatGPT 5.1 | Gemini 3 Pro |
| :---- | :---- | :---- | :---- |
| **Associativity & Commutativity** | **Rearrangement:** Examples 1-4 prove that order doesn't matter in multiplication (e.g., a \* b \* c \= b \* a \* c) using mul\_comm and mul\_assoc. | **Yes.** Analyzed Examples 1-4 individually, explaining they "reorder the factors" using commutativity and associativity. | **Yes.** Grouped them under "Rearrangement of Multiplication," noting they rely on axioms that real multiplication is commutative and associative. |
| **Hypothesis Substitution** | **Rewriting Hypotheses:** Examples 5-6 demonstrate replacing terms inside assumptions (e.g., rw \[hyp'\] at hyp) to solve systems like c \= d \* a \+ b. | **Yes.** Detailed how hyp and hyp' are used to substitute values like b \= a \* d to simplify expressions. | **Yes.** Described as "Substitution and Linear Arithmetic," explaining how to substitute known values into equations. |
| **calc Blocks** | **Structured Proofs:** Examples 7-8 introduce calc blocks to write step-by-step, readable derivations resembling pen-and-paper math. | **Yes.** Noted that calc makes "each intermediate step visible" and acts as a "structured derivation." | **Yes.** Dedicated a section to "The calc Mode," explaining it allows step-by-step derivations. |
| **ring Tactic** | **Automation:** Examples 9-11 introduce the ring tactic to automatically solve algebraic equalities without manual steps. | **Yes.** Explained that ring "automatically solve\[s\] polynomial identities" and "normalizes both sides." | **Yes.** Described ring as "powerful automation" that replaces manual rewriting for commutative rings. |
| **Difference of Squares** | **Manual Proof:** Example 12 proves (a \+ b)(a \- b) \= a^2 \- b^2 manually using distributive laws (mul\_sub, add\_mul). | **Yes.** Walked through the proof expansion: (a \+ b)a \- (a \+ b)b ... \= a^2 \- b^2. | **Yes.** Identified as the "classic 'difference of two squares' expansion" using the FOIL method. |
| **Overall Goal** | **Pedagogical Purpose:** A tutorial on **rewriting techniques** (rw, calc, ring) rather than a list of new theorems. | **Yes.** Correctly identified it as a "practice sheet" to get comfortable with rewriting and algebra. | **Yes.** Correctly identified it as a "tutorial or exercise sheet demonstrating equality rewriting." |

[https://chatgpt.com/share/69380e3a-d4ac-8012-8503-1e7de0813d1e](https://chatgpt.com/share/69380e3a-d4ac-8012-8503-1e7de0813d1e)

[https://gemini.google.com/share/81df1ecf7b80](https://gemini.google.com/share/81df1ecf7b80)

**02IffIfAnd.lean**   
**([https://github.com/leanprover-community/tutorials4/blob/master/Tutorials/Solutions/02IffIfAnd.lean](https://github.com/leanprover-community/tutorials4/blob/master/Tutorials/Solutions/02IffIfAnd.lean))**

 This file contains **exercises and explanations focused on how to apply logical equivalences and rewriting techniques by transforming statements into equivalent forms using `Iff` rewriting.**

| Theorem / Concept | Explanation (Based on File) | ChatGPT 5.1 | Gemini 3 Pro |
| :---- | :---- | :---- | :---- |
| **Monotonicity of Addition** | **Adding preserves order:** a \<= b implies a \+ c \<= b \+ c. Proved via sub\_nonneg or library lemmas. | **Yes.** Identified as "Adding the same number preserves \<=" and noted it's a standard order-preserving operation. | **Yes.** Identified as "Monotonicity of Addition" and explained adding the same value preserves the inequality. |
| **Multiplication & Order** | **Sign matters:** Multiplying by c \>= 0 preserves order; multiplying by c \<= 0 reverses it. | **Yes.** Separated into two sections (5 & 6\) for nonnegative (preserves) and nonpositive (reverses) cases. | **Yes.** Separated into "Multiplication by Non-negative" and "Multiplication by Non-positive," noting the reversal. |
| **Logic: AND & Implication** | **Logical structural manipulation:** Proves P /\\ Q \-\> Q /\\ P and the Currying equivalence (P /\\ Q \-\> R) \<-\> (P \-\> Q \-\> R). | **Yes.** Identified "Commutativity of /" and "Equivalence between uncurried and curried forms." | **Yes.** Identified "Implication & Conjunction," specifically mentioning commutativity and currying. |
| **Forward vs. Backward** | **Proof direction:** The file explicitly contrasts forward reasoning (have, calc) with backward reasoning (apply, rw). | **Yes.** Discussed the progression of styles: "Rewriting," "Chaining with calc," "Using lemmas directly." | **Yes.** Explicitly noted the "manual" sub\_nonneg method vs. calc blocks vs. automation. |
| **linarith Tactic** | **Automation:** linarith is introduced to instantly solve linear inequalities that were previously done manually. | **Yes.** Noted that "same inequalities proved with automation (linarith)" replaces tedious manual steps. | **Yes.** Highlighted linarith as the "Automation Method" that solves tedious proofs instantly. |
| **GCD & Divisibility** | **Number Theory:** Proves a divides b if and only if gcd(a, b) \= a using dvd\_gcd\_iff and antisymmetry. | **Yes.** Correctly identified the theorem: a divides b iff gcd(a, b) \= a. | **Yes.** Correctly identified the theorem: a divides b iff GCD of a and b is equal to a. |
| **Overall Goal** | **Pedagogical Purpose:** A tutorial on **structured reasoning** (logic, forward/backward proofs) and automation. | **Yes.** "Training ground for working with inequalities, logical structure... using both low-level... and higher-level automation." | **Yes.** "Tutorial or drill sheet demonstrating how to formalize standard mathematical proofs... progresses from manual... to high-level." |

[https://chatgpt.com/share/69380e7c-1ae8-8012-93e8-0f16684d41ab](https://chatgpt.com/share/69380e7c-1ae8-8012-93e8-0f16684d41ab)

[https://gemini.google.com/share/3ab49a2818c6](https://gemini.google.com/share/3ab49a2818c6)

**03ForallOr.lean** 

**([https://github.com/leanprover-community/tutorials4/blob/master/Tutorials/Solutions/03ForallOr.lean](https://github.com/leanprover-community/tutorials4/blob/master/Tutorials/Solutions/03ForallOr.lean))**

 This file contains **using the universal quantifier ∀ and disjunction ∨ in Lean proofs, applying tactics like intro, rw, and case splits to properties of real functions and algebraic equalities.** 

| Theorem / Concept | Explanation (Based on File) | ChatGPT 5.1 | Gemini 3 Pro |
| :---- | :---- | :---- | :---- |
| **Even/Odd Functions** | **Parity Preservation:** Proves sum of even functions is even, composition with even is even, and composition of odds is odd. | **Yes.** Detailed the "Proof idea" for each case (Sum, Composition Even, Composition Odd). | **Yes.** Grouped under "Function Parity," explaining why each holds (e.g., inner function "absorbs" the negative). |
| **Monotonicity Composition** | **Chain Rule for Order:** Proves composition of non-decreasing functions is non-decreasing. Also, non-decreasing composed with non-increasing is non-increasing. | **Yes.** Correctly identified both cases and the logic: f preserves order, g flips it. | **Yes.** Grouped under "Function Monotonicity," noting g reverses the order in the second case. |
| **Forward vs. Backward** | **Proof Styles:** Explicitly contrasts Forward reasoning (intro, have, specialize) vs. Backward reasoning (apply). | **Yes.** Noted the file shows stylistic variants: have step1, specialize, and apply. | **Yes.** Discussed "Tactic Mode vs. Term Mode" and the functional programming style. |
| **Algebraic Disjunction** | **Case Splitting:** Proves a \= a \* b \-\> a \= 0 or b \= 1 and x^2 \= y^2 \-\> x \= y or x \= \-y using mul\_eq\_zero. | **Yes.** Walked through the factorization steps (e.g., a(1-b)=0) and the use of mul\_eq\_zero. | **Yes.** Grouped under "Algebraic Logic" and identified the zero-product property logic. |
| **Order Disjunction** | **Advanced Logic:** Proves NonDecreasing equivalence (\<= vs \<) and the fixed point theorem (f(f(x)) \= x \-\> f(x) \= x). | **Yes.** Detailed the "Nondecreasing involution" proof, explaining the contradiction in both cases (f(x) \< x and x \< f(x)). | **Yes.** Identified the "Equivalence of Monotonicity" and "Fixed Point of Non-Decreasing Involutions." |
| **Overall Goal** | **Pedagogical Purpose:** A tutorial on **Quantifiers** (forall) and **Disjunction** (or) utilizing functions and case splits. | **Yes.** Described it as a collection of lemmas about parity/monotonicity illustrating proof patterns like rcases and calc. | **Yes.** Described it as a tutorial teaching calc blocks, logic handling (rcases), and automation. |

[https://chatgpt.com/share/69380ea1-e62c-8012-b30a-21a49c9fb080](https://chatgpt.com/share/69380ea1-e62c-8012-b30a-21a49c9fb080)

[https://gemini.google.com/share/78da1d1de5ce](https://gemini.google.com/share/78da1d1de5ce)

**04Exists.lean** 

**([https://github.com/leanprover-community/tutorials4/blob/master/Tutorials/Solutions/04Exists.lean](https://github.com/leanprover-community/tutorials4/blob/master/Tutorials/Solutions/04Exists.lean))**

 This file contains **exercises on using existential quantifiers, focusing on constructing witnesses with `use`, extracting them with `rcases`, and applying these techniques to divisibility and surjectivity.**

| Theorem / Concept | Explanation (Based on File) | ChatGPT 5.1 | Gemini 3 Pro |
| :---- | :---- | :---- | :---- |
| **Basic Existence** | **Witnesses:** Proves 8 \= 2 \* n by providing n \= 4 (use 4\) and proves n \= k \+ 1 implies n \> 0\. | **Yes.** Identified as "8 is even" and "successor is positive," noting the explicit witness n=4. | **Yes.** Identified as "Existence of an Even Number" and "Positivity of Successors," noting the use of witness 4\. |
| **Divisibility Transitivity** | **Unpacking Definitions:** Proves if a divides b and b divides c, then a divides c. Uses rcases to extract multipliers. | **Yes.** Identified as "Transitivity of divisibility" and sketched the algebra: c \= a(k l). | **Yes.** Identified as "Transitivity of Divisibility" and explained substituting b to get a \* (k \* l). |
| **Divisibility of Sums** | **Linearity:** Proves if a divides b and c, it divides b \+ c. Shows use of ring to simplify a(k \+ l). | **Yes.** Identified "Algebraic manipulation of sums of multiples" and noted the curried form variation. | **Yes.** Identified as "Divisibility of Sums," noting it requires proving a divides b \+ c. |
| **Zero Divisor** | **Iff Proof:** Proves 0 divides a if and only if a \= 0\. Requires handling both forward and backward logic. | **Yes.** Identified as "Zero divides a if and only if a \= 0," explaining both forward and backward logic. | **Yes.** Identified as "Zero Divisor Property," noting the "if and only if" structure. |
| **Surjectivity Logic** | **Function Composition:** Proves Surjective (g o f) implies Surjective g, and Surjective f and g implies Surjective (g o f). | **Yes.** Explained the "Proof idea": constructing preimages (w or x) using the definitions. | **Yes.** Broken down into "Surjectivity of Outer Function" and "Composition of Surjective Functions." |
| **Overall Goal** | **Pedagogical Purpose:** A tutorial on **Existential Logic** (exists), using use to provide witnesses and rcases to extract them. | **Yes.** Described it as a "tour of standard proof patterns" for handling existentials and witnesses. | **Yes.** Described it as covering "Elementary Number Theory" and "Function Theory" to teach "Constructive Existence." |

[https://chatgpt.com/share/69380ed7-ae24-8012-b355-314fb71e7b6f](https://chatgpt.com/share/69380ed7-ae24-8012-b355-314fb71e7b6f)

[https://gemini.google.com/share/3385ec7db8f5](https://gemini.google.com/share/3385ec7db8f5)

