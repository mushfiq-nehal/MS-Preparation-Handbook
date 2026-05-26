# 📘 MSc Admission Prep — Subject 11: Discrete Mathematics
### 🎯 JUST-Style Exam Handbook | Tier B — Moderately Important

> **Goal:** Focused revision of discrete math topics most likely to appear in MSc admission exams. Intuition-first, with worked examples and exam tips.

---

## 📋 Table of Contents

| # | Topic |
|---|-------|
| 1 | [Set Theory](#1-set-theory) |
| 2 | [Propositional Logic & Truth Tables](#2-propositional-logic--truth-tables) |
| 3 | [Graph Theory](#3-graph-theory) |
| 4 | [Recurrence Relations](#4-recurrence-relations) |
| 5 | [Permutations & Combinations](#5-permutations--combinations) |
| 6 | [Mathematical Induction](#6-mathematical-induction) |

---

# 1. Set Theory

## 💡 Intuition First

> A **set** is a collection of distinct objects. Like a bag of unique items — no duplicates, no order.

---

## 📐 Set Notation & Operations

```
Sets: A = {1, 2, 3, 4},  B = {3, 4, 5, 6}
Universal set U = {1, 2, 3, 4, 5, 6, 7, 8}

Union:        A ∪ B = {1,2,3,4,5,6}     (in A OR B)
Intersection: A ∩ B = {3,4}             (in A AND B)
Difference:   A - B = {1,2}             (in A but NOT B)
Complement:   A' = U - A = {5,6,7,8}   (NOT in A)
Symmetric Diff: A △ B = {1,2,5,6}      (in A or B but NOT both)
```

### Venn Diagram

```
    ┌─────────────────────────────┐  U
    │   ┌───────┐   ┌───────┐    │
    │   │  A    │   │    B  │    │
    │   │ 1,2   │3,4│  5,6  │7,8 │
    │   └───────┘   └───────┘    │
    └─────────────────────────────┘
         A∩B = {3,4}
```

### Set Laws

```
Commutative:   A ∪ B = B ∪ A          A ∩ B = B ∩ A
Associative:   (A∪B)∪C = A∪(B∪C)     (A∩B)∩C = A∩(B∩C)
Distributive:  A∪(B∩C) = (A∪B)∩(A∪C)
               A∩(B∪C) = (A∩B)∪(A∩C)
De Morgan's:   (A∪B)' = A'∩B'
               (A∩B)' = A'∪B'
Identity:      A∪∅ = A    A∩U = A
Complement:    A∪A' = U   A∩A' = ∅
```

### Cardinality (Inclusion-Exclusion)

```
|A ∪ B| = |A| + |B| - |A ∩ B|

|A ∪ B ∪ C| = |A| + |B| + |C|
             - |A∩B| - |B∩C| - |A∩C|
             + |A∩B∩C|

Example: 100 students, 60 study Math, 50 study CS, 30 study both.
  |Math ∪ CS| = 60 + 50 - 30 = 80 study at least one
  Neither = 100 - 80 = 20
```

---

## ⚡ One-Minute Recap

- Union: A OR B | Intersection: A AND B | Difference: A not B
- De Morgan's: (A∪B)' = A'∩B' | (A∩B)' = A'∪B'
- Inclusion-exclusion: |A∪B| = |A|+|B|-|A∩B|

---

## 📝 Probable Exam Questions

> **5-mark:** Given A={1,2,3,4,5}, B={3,4,5,6,7}, U={1..10}, find A∪B, A∩B, A-B, A'.
> **Calculate:** In a class of 50, 30 like cricket, 25 like football, 10 like both. How many like neither?

---

---

# 2. Propositional Logic & Truth Tables

## 💡 Intuition First

> Propositional logic is the math of **true/false statements**. Like Boolean algebra but for reasoning. "If it rains, I carry an umbrella" — this is a logical implication.

---

## 📐 Logical Connectives

| Symbol | Name | Meaning | True when |
|--------|------|---------|-----------|
| ¬p | NOT | Negation | p is false |
| p ∧ q | AND | Conjunction | both true |
| p ∨ q | OR | Disjunction | at least one true |
| p → q | Implication | If p then q | p false OR q true |
| p ↔ q | Biconditional | p iff q | both same value |
| p ⊕ q | XOR | Exclusive or | exactly one true |

---

## 📐 Truth Tables

### Implication (p → q) — Most Tricky!

```
p │ q │ p→q
──┼───┼─────
T │ T │  T    (true implies true = true)
T │ F │  F    (true implies false = false — only false case!)
F │ T │  T    (false implies true = true — vacuously true)
F │ F │  T    (false implies false = true — vacuously true)

Memory trick: p→q is FALSE only when p=T and q=F
              "A true premise leading to a false conclusion is invalid"
```

### Biconditional (p ↔ q)

```
p │ q │ p↔q
──┼───┼─────
T │ T │  T
T │ F │  F
F │ T │  F
F │ F │  T    (true when both same)

p↔q = (p→q) ∧ (q→p)
```

### Full Truth Table Example

```
Prove: p → q ≡ ¬p ∨ q

p │ q │ ¬p │ p→q │ ¬p∨q
──┼───┼────┼─────┼──────
T │ T │  F │  T  │  T   ✅
T │ F │  F │  F  │  F   ✅
F │ T │  T │  T  │  T   ✅
F │ F │  T │  T  │  T   ✅

Columns p→q and ¬p∨q are identical → they are logically equivalent!
```

---

## 📐 Logical Equivalences

```
De Morgan's Laws:
  ¬(p ∧ q) ≡ ¬p ∨ ¬q
  ¬(p ∨ q) ≡ ¬p ∧ ¬q

Implication:
  p → q ≡ ¬p ∨ q
  p → q ≡ ¬q → ¬p  (contrapositive — equivalent!)

Contrapositive vs Converse vs Inverse:
  Original:      p → q
  Contrapositive: ¬q → ¬p  (equivalent to original ✅)
  Converse:       q → p    (NOT equivalent ❌)
  Inverse:        ¬p → ¬q  (NOT equivalent ❌)
```

---

## 📐 Tautology, Contradiction, Contingency

```
Tautology:    Always TRUE regardless of variable values
              Example: p ∨ ¬p (always true)

Contradiction: Always FALSE
              Example: p ∧ ¬p (always false)

Contingency:  Sometimes true, sometimes false
              Example: p ∧ q
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** p→q is FALSE only when p=T and q=F. All other cases are TRUE.
> 🚫 **Mistake 2:** Contrapositive (¬q→¬p) is equivalent to original. Converse (q→p) is NOT.
> 🚫 **Mistake 3:** p↔q is true when BOTH have the same truth value (both T or both F).

---

## ⚡ One-Minute Recap

- AND: both true | OR: at least one | NOT: flip
- p→q: false ONLY when p=T, q=F
- p↔q: true when both same
- Contrapositive ≡ original | Converse ≠ original
- Tautology: always true | Contradiction: always false

---

## 📝 Probable Exam Questions

> **5-mark:** Construct a truth table for (p→q) ∧ (q→r) → (p→r). Is it a tautology?
> **Short note:** What is the contrapositive of "If it rains, the ground is wet"?
> **Prove:** Show that p→q ≡ ¬p∨q using a truth table.

---

---

# 3. Graph Theory

## 💡 Intuition First

> A **graph** is a set of vertices (nodes) connected by edges. Like a map of cities connected by roads, or a social network of people connected by friendships.

---

## 📐 Graph Terminology

```
G = (V, E)
V = vertices (nodes): {A, B, C, D}
E = edges: {(A,B), (B,C), (C,D), (A,D)}

Degree of vertex v: number of edges incident to v
  In directed graph: in-degree + out-degree

Path: sequence of vertices connected by edges
Cycle: path that starts and ends at same vertex
Connected graph: path exists between every pair of vertices
Tree: connected graph with no cycles (n vertices, n-1 edges)
```

### Types of Graphs

| Type | Description |
|------|-------------|
| **Undirected** | Edges have no direction |
| **Directed (Digraph)** | Edges have direction |
| **Weighted** | Edges have weights/costs |
| **Complete (Kₙ)** | Every vertex connected to every other |
| **Bipartite** | Vertices split into 2 sets, edges only between sets |
| **Tree** | Connected, acyclic, n-1 edges |

---

## 📐 Graph Representations

### Adjacency Matrix

```
Graph: A-B, A-C, B-C, B-D

     A  B  C  D
A  [ 0  1  1  0 ]
B  [ 1  0  1  1 ]
C  [ 1  1  0  0 ]
D  [ 0  1  0  0 ]

Space: O(V²)
Check edge: O(1)
Find neighbors: O(V)
```

### Adjacency List

```
A: [B, C]
B: [A, C, D]
C: [A, B]
D: [B]

Space: O(V + E)
Check edge: O(degree)
Find neighbors: O(degree)
```

---

## 📐 Euler Path & Euler Circuit

```
Euler Path: visits every EDGE exactly once
  Condition: exactly 0 or 2 vertices with odd degree

Euler Circuit: Euler path that starts and ends at same vertex
  Condition: ALL vertices have even degree

Hamiltonian Path: visits every VERTEX exactly once
Hamiltonian Circuit: Hamiltonian path returning to start
  (NP-complete — no efficient algorithm known)
```

---

## 📐 Graph Coloring

```
Chromatic number χ(G): minimum colors needed to color vertices
                       such that no adjacent vertices share a color

Bipartite graph: χ = 2 (always 2-colorable)
Complete graph Kₙ: χ = n

4-Color Theorem: Any planar graph can be colored with 4 colors
```

---

## ⚡ One-Minute Recap

- Graph: vertices + edges | Degree: edges per vertex
- Tree: connected + acyclic + n-1 edges
- Euler circuit: all even degrees | Euler path: exactly 2 odd degrees
- Adjacency matrix: O(V²) space | Adjacency list: O(V+E) space

---

## 📝 Probable Exam Questions

> **5-mark:** Given a graph, find: degree of each vertex, adjacency matrix, whether Euler circuit exists.
> **Short note:** What is the difference between Euler path and Hamiltonian path?

---

---

# 4. Recurrence Relations

## 💡 Intuition First

> A recurrence relation defines a sequence where each term depends on previous terms. Like Fibonacci — each number is the sum of the two before it.

---

## 📐 Common Recurrences

```
Linear recurrence:
  T(n) = T(n-1) + c        → T(n) = O(n)
  T(n) = T(n-1) + n        → T(n) = O(n²)

Divide and conquer:
  T(n) = 2T(n/2) + n       → T(n) = O(n log n)  [Merge sort]
  T(n) = T(n/2) + 1        → T(n) = O(log n)    [Binary search]
  T(n) = T(n-1) + T(n-2)   → T(n) = O(2ⁿ)      [Naive Fibonacci]
```

### Solving by Substitution

```
T(n) = T(n-1) + 1,  T(1) = 1

T(n) = T(n-1) + 1
     = T(n-2) + 1 + 1
     = T(n-3) + 1 + 1 + 1
     = T(1) + (n-1)×1
     = 1 + n - 1
     = n
→ T(n) = O(n)
```

### Master Theorem (Review)

```
T(n) = aT(n/b) + f(n)

Compare f(n) with n^(log_b a):
  Case 1: f(n) = O(n^(log_b a - ε)) → T(n) = Θ(n^log_b a)
  Case 2: f(n) = Θ(n^log_b a)       → T(n) = Θ(n^log_b a · log n)
  Case 3: f(n) = Ω(n^(log_b a + ε)) → T(n) = Θ(f(n))

Examples:
  T(n) = 2T(n/2) + n: a=2,b=2, n^log₂2=n → Case 2 → O(n log n)
  T(n) = 4T(n/2) + n: a=4,b=2, n^log₂4=n² → Case 1 → O(n²)
```

---

## ⚡ One-Minute Recap

- Recurrence: each term defined by previous terms
- Solve by substitution: expand until base case
- Master theorem: T(n)=aT(n/b)+f(n) → compare f(n) with n^log_b(a)

---

## 📝 Probable Exam Questions

> **5-mark:** Solve T(n) = 2T(n/2) + n using the Master Theorem.
> **Solve:** Find closed form for T(n) = T(n-1) + 2, T(1) = 1.

---

# 5. Permutations & Combinations

## 💡 Intuition First

> **Permutation:** Order matters — arranging books on a shelf.
> **Combination:** Order doesn't matter — choosing a committee.

---

## 📐 Formulas

```
Permutation (order matters):
  P(n, r) = n! / (n-r)!
  "Choose r from n, order matters"

  Example: How many ways to arrange 3 books from 5?
  P(5,3) = 5!/(5-3)! = 5!/2! = 120/2 = 60

Combination (order doesn't matter):
  C(n, r) = n! / (r! × (n-r)!)  = P(n,r) / r!
  "Choose r from n, order doesn't matter"

  Example: How many ways to choose 3 students from 5?
  C(5,3) = 5!/(3!×2!) = 120/(6×2) = 10

Relationship: C(n,r) = P(n,r) / r!
```

### Pascal's Triangle

```
C(n,r) = C(n-1,r-1) + C(n-1,r)

         C(0,0)=1
       C(1,0) C(1,1)
     C(2,0) C(2,1) C(2,2)
   C(3,0) C(3,1) C(3,2) C(3,3)

         1
        1 1
       1 2 1
      1 3 3 1
     1 4 6 4 1
```

### Special Cases

```
C(n,0) = 1    (choose none: 1 way)
C(n,n) = 1    (choose all: 1 way)
C(n,1) = n    (choose one: n ways)
C(n,r) = C(n, n-r)  (symmetry)

Permutation with repetition: nʳ
  (r items chosen from n, repetition allowed)
  Example: 4-digit PIN from 0-9: 10⁴ = 10000

Combination with repetition: C(n+r-1, r)
```

---

## ✏️ Worked Examples

```
Example 1: How many 3-letter passwords from {A,B,C,D,E}?
  With repetition: 5³ = 125
  Without repetition: P(5,3) = 60

Example 2: Committee of 4 from 10 people?
  C(10,4) = 10!/(4!×6!) = 210

Example 3: How many ways to arrange "MISSISSIPPI"?
  Total letters: 11
  M=1, I=4, S=4, P=2
  = 11! / (1! × 4! × 4! × 2!)
  = 39916800 / (1 × 24 × 24 × 2)
  = 34650
```

---

## ⚡ One-Minute Recap

- Permutation P(n,r) = n!/(n-r)! — order matters
- Combination C(n,r) = n!/(r!(n-r)!) — order doesn't matter
- C(n,r) = C(n, n-r) — symmetry
- With repetition: nʳ (permutation) | C(n+r-1,r) (combination)

---

## 📝 Probable Exam Questions

> **Calculate:** How many ways to choose a team of 5 from 12 players?
> **Calculate:** How many 4-digit numbers can be formed from {1,2,3,4,5} without repetition?
> **Short note:** What is the difference between permutation and combination?

---

---

# 6. Mathematical Induction

## 💡 Intuition First

> Mathematical induction is like a chain of dominoes — if the first one falls (base case) and each domino knocks the next (inductive step), then ALL dominoes fall.

---

## 📐 Proof by Induction — Steps

```
To prove: P(n) is true for all n ≥ 1

Step 1 — Base Case:
  Show P(1) is true (or P(0), depending on problem)

Step 2 — Inductive Hypothesis:
  Assume P(k) is true for some arbitrary k ≥ 1

Step 3 — Inductive Step:
  Using the hypothesis, prove P(k+1) is true

Conclusion:
  By induction, P(n) is true for all n ≥ 1
```

---

## ✏️ Worked Example 1: Sum Formula

```
Prove: 1 + 2 + 3 + ... + n = n(n+1)/2

Base Case (n=1):
  LHS = 1
  RHS = 1(1+1)/2 = 1 ✅

Inductive Hypothesis:
  Assume 1+2+...+k = k(k+1)/2 for some k ≥ 1

Inductive Step (prove for k+1):
  1+2+...+k+(k+1)
  = k(k+1)/2 + (k+1)    [using hypothesis]
  = (k+1)[k/2 + 1]
  = (k+1)(k+2)/2
  = (k+1)((k+1)+1)/2    ✅ matches formula with n=k+1

Conclusion: True for all n ≥ 1 ✎
```

---

## ✏️ Worked Example 2: Sum of Squares

```
Prove: 1² + 2² + ... + n² = n(n+1)(2n+1)/6

Base Case (n=1):
  LHS = 1
  RHS = 1(2)(3)/6 = 1 ✅

Inductive Step:
  Assume true for k: 1²+...+k² = k(k+1)(2k+1)/6
  Prove for k+1:
  1²+...+k²+(k+1)²
  = k(k+1)(2k+1)/6 + (k+1)²
  = (k+1)[k(2k+1)/6 + (k+1)]
  = (k+1)[k(2k+1) + 6(k+1)] / 6
  = (k+1)[2k²+k+6k+6] / 6
  = (k+1)[2k²+7k+6] / 6
  = (k+1)(k+2)(2k+3) / 6
  = (k+1)((k+1)+1)(2(k+1)+1) / 6 ✅
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Forgetting the base case — induction without base case proves nothing.
> 🚫 **Mistake 2:** Assuming what you're trying to prove (circular reasoning).
> 🚫 **Mistake 3:** The inductive step must use the hypothesis to prove P(k+1), not just verify it.

---

## ⚡ One-Minute Recap

- Induction: base case + inductive step → true for all n
- Base case: verify P(1) directly
- Inductive step: assume P(k), prove P(k+1)
- Common formulas: Σn = n(n+1)/2 | Σn² = n(n+1)(2n+1)/6 | Σn³ = [n(n+1)/2]²

---

## 📝 Probable Exam Questions

> **5-mark:** Prove by induction: 1+2+3+...+n = n(n+1)/2.
> **5-mark:** Prove by induction: 2⁰+2¹+2²+...+2ⁿ = 2ⁿ⁺¹-1.

---

# 🏁 Quick Revision — Discrete Mathematics

## Key Formulas

```
Set theory:    |A∪B| = |A|+|B|-|A∩B|
Permutation:   P(n,r) = n!/(n-r)!
Combination:   C(n,r) = n!/(r!(n-r)!)
Sum formula:   Σk = n(n+1)/2
Sum squares:   Σk² = n(n+1)(2n+1)/6
Implication:   p→q ≡ ¬p∨q
Contrapositive: p→q ≡ ¬q→¬p
```

---

> 📌 **End of Subject 11: Discrete Mathematics**

---
