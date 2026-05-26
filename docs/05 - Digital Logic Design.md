# 📘 MSc Admission Prep — Subject 05: Digital Logic Design
### 🎯 JUST-Style Exam Handbook | Fast Revision Edition

> **Goal:** Visual, exam-focused revision of Boolean algebra, logic circuits, K-maps, and sequential logic. Every topic includes truth tables, circuit diagrams, and worked examples.

---

## 📋 Table of Contents

| # | Topic | Tier |
|---|-------|------|
| 1 | [Boolean Algebra & Laws](#1-boolean-algebra--laws) | 🔴 Must Master |
| 2 | [SOP & POS Forms](#2-sop--pos-forms) | 🔴 Must Master |
| 3 | [Karnaugh Maps (K-Map)](#3-karnaugh-maps-k-map) | 🔴 Must Master |
| 4 | [Logic Gates](#4-logic-gates) | 🔴 Must Master |
| 5 | [Combinational Circuits — Adders](#5-combinational-circuits--adders) | 🔴 Must Master |
| 6 | [Multiplexer & Demultiplexer](#6-multiplexer--demultiplexer) | 🔴 Must Master |
| 7 | [Encoder & Decoder](#7-encoder--decoder) | 🔴 Must Master |
| 8 | [Flip-Flops](#8-flip-flops) | 🔴 Must Master |
| 9 | [Counters](#9-counters) | 🔴 Must Master |
| 10 | [Registers](#10-registers) | 🔴 Must Master |

---

---

# 1. Boolean Algebra & Laws

## 💡 Intuition First

> Boolean algebra is the math of **true/false decisions**. Every digital circuit — from a light switch to a CPU — is built on these rules. Instead of numbers, we work with 0 (false/off) and 1 (true/on).

**Real-world analogy:** A light turns on (1) only if switch A AND switch B are both on. That's `A · B`. A light turns on if switch A OR switch B is on. That's `A + B`.

---

## 📐 Basic Operations

| Operation | Symbol | Meaning | Example |
|-----------|--------|---------|---------|
| **AND** | · or ∧ | Both must be 1 | 1·1=1, 1·0=0 |
| **OR** | + or ∨ | At least one must be 1 | 1+0=1, 0+0=0 |
| **NOT** | ¯ or ¬ | Invert | 0̄=1, 1̄=0 |
| **NAND** | ↑ | NOT AND | (1·1)̄=0 |
| **NOR** | ↓ | NOT OR | (1+0)̄=0 |
| **XOR** | ⊕ | Exactly one is 1 | 1⊕0=1, 1⊕1=0 |
| **XNOR** | ⊙ | Both same | 1⊙1=1, 1⊙0=0 |

---

## 📐 Boolean Laws & Theorems

### Identity Laws
```
A + 0 = A          A · 1 = A
A + 1 = 1          A · 0 = 0
```

### Complement Laws
```
A + Ā = 1          A · Ā = 0
Ā̄ = A              (double complement)
```

### Idempotent Laws
```
A + A = A          A · A = A
```

### Commutative Laws
```
A + B = B + A      A · B = B · A
```

### Associative Laws
```
(A+B)+C = A+(B+C)      (A·B)·C = A·(B·C)
```

### Distributive Laws
```
A·(B+C) = A·B + A·C    A+(B·C) = (A+B)·(A+C)
```

### Absorption Laws
```
A + A·B = A            A·(A+B) = A
```

### De Morgan's Theorems ⭐ (Most Important!)
```
(A + B)̄ = Ā · B̄        "Break the bar, change the sign"
(A · B)̄ = Ā + B̄

Mnemonic: "Break the line, change the sign"
  NOR  = AND of complements
  NAND = OR of complements
```

---

## ✏️ Boolean Simplification — Worked Examples

### Example 1
```
Simplify: F = AB + AB̄

F = AB + AB̄
  = A(B + B̄)      [Distributive]
  = A · 1          [Complement: B + B̄ = 1]
  = A              [Identity]
```

### Example 2
```
Simplify: F = A + ĀB

F = A + ĀB
  = (A + Ā)(A + B)    [Distributive: A+(B·C) = (A+B)·(A+C)]
  = 1 · (A + B)        [Complement]
  = A + B              [Identity]
```

### Example 3
```
Simplify: F = ABC + ABC̄ + AB̄C

F = ABC + ABC̄ + AB̄C
  = AB(C + C̄) + AB̄C    [Factor AB]
  = AB·1 + AB̄C          [Complement]
  = AB + AB̄C            [Identity]
  = A(B + B̄C)           [Factor A]
  = A(B + C)             [Absorption: B + B̄C = B + C]
```

---

## ⚖️ De Morgan's — Application

```
Convert NAND to basic gates:
  F = (AB)̄ = Ā + B̄     [De Morgan's]

Convert NOR to basic gates:
  F = (A+B)̄ = Ā · B̄    [De Morgan's]

Complement a function:
  F = AB + C̄D
  F̄ = (AB + C̄D)̄
    = (AB)̄ · (C̄D)̄       [De Morgan's on OR]
    = (Ā+B̄) · (C+D̄)     [De Morgan's on each AND]
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** De Morgan's: `(A+B)̄ ≠ Ā + B̄` — it equals `Ā · B̄`. Change + to · when breaking the bar.
> 🚫 **Mistake 2:** `A + AB ≠ AB` — it equals `A` (absorption law).
> 🚫 **Mistake 3:** XOR: `A ⊕ A = 0` and `A ⊕ 0 = A` and `A ⊕ 1 = Ā`.
> 🚫 **Mistake 4:** Boolean + is OR, not arithmetic addition. `1 + 1 = 1` (not 2).

---

## 🎯 Exam Tips

> 💡 **De Morgan's theorem** is the most tested Boolean law — know both forms cold.
> 💡 Simplification steps: always show each law applied.
> 💡 Absorption: `A + AB = A` and `A(A+B) = A` — very useful shortcuts.
> 💡 XOR properties: `A⊕A=0`, `A⊕0=A`, `A⊕1=Ā`, `A⊕B=B⊕A`.

---

## ⚡ One-Minute Recap

- AND: both 1 → 1 | OR: any 1 → 1 | NOT: invert
- De Morgan's: `(A+B)̄ = Ā·B̄` and `(AB)̄ = Ā+B̄`
- Absorption: `A+AB=A` and `A(A+B)=A`
- Distributive: `A(B+C) = AB+AC` and `A+(BC) = (A+B)(A+C)`

---

## 📝 Probable Exam Questions

> **5-mark:** Simplify `F = AB̄C + ABC + AB̄C̄` using Boolean algebra. Show each step.
> **Short note:** State and prove De Morgan's theorems.
> **Simplify:** `F = (A+B)(A+B̄)` using Boolean algebra.
> **Apply:** Use De Morgan's to find the complement of `F = AB + C̄D`.

---

---

# 2. SOP & POS Forms

## 💡 Intuition First

> Every Boolean function can be expressed in two standard forms:
> - **SOP (Sum of Products):** OR of AND terms — "the function is 1 when THIS combination OR THAT combination is true"
> - **POS (Product of Sums):** AND of OR terms — "the function is 1 only when ALL these conditions hold"

**Real-world analogy:**
- SOP = "You pass if (you score ≥ 50 AND attend ≥ 75%) OR (you score ≥ 80%)"
- POS = "You pass only if (you score ≥ 50) AND (you attend ≥ 75%) AND (no cheating)"

---

## 📐 Minterms and Maxterms

```
For n variables, there are 2ⁿ minterms and 2ⁿ maxterms.

For 2 variables A, B:
Row │ A │ B │ Minterm (mᵢ)  │ Maxterm (Mᵢ)
────┼───┼───┼───────────────┼──────────────
 0  │ 0 │ 0 │ m₀ = Ā·B̄     │ M₀ = A+B
 1  │ 0 │ 1 │ m₁ = Ā·B      │ M₁ = A+B̄
 2  │ 1 │ 0 │ m₂ = A·B̄     │ M₂ = Ā+B
 3  │ 1 │ 1 │ m₃ = A·B      │ M₃ = Ā+B̄

Minterm: product term that is 1 for exactly ONE row
Maxterm: sum term that is 0 for exactly ONE row
```

> 🔑 **Key relationship:** mᵢ and Mᵢ are complements: `mᵢ = M̄ᵢ`

---

## 📐 Canonical SOP (Sum of Minterms)

> Write the function as OR of all minterms where output = 1.

```
Truth table for F(A,B,C):
Row │ A │ B │ C │ F
────┼───┼───┼───┼───
 0  │ 0 │ 0 │ 0 │ 0
 1  │ 0 │ 0 │ 1 │ 1  ← minterm m₁
 2  │ 0 │ 1 │ 0 │ 0
 3  │ 0 │ 1 │ 1 │ 1  ← minterm m₃
 4  │ 1 │ 0 │ 0 │ 1  ← minterm m₄
 5  │ 1 │ 0 │ 1 │ 0
 6  │ 1 │ 1 │ 0 │ 1  ← minterm m₆
 7  │ 1 │ 1 │ 1 │ 0

Canonical SOP:
F = m₁ + m₃ + m₄ + m₆
F = Ā·B̄·C + Ā·B·C + A·B̄·C̄ + A·B·C̄
F = Σm(1,3,4,6)
```

---

## 📐 Canonical POS (Product of Maxterms)

> Write the function as AND of all maxterms where output = 0.

```
From same truth table, F = 0 at rows 0, 2, 5, 7:

Canonical POS:
F = M₀ · M₂ · M₅ · M₇
F = (A+B+C)(A+B̄+C)(Ā+B+C̄)(Ā+B̄+C̄)
F = ΠM(0,2,5,7)
```

> 🔑 **Shortcut:** SOP uses rows where F=1 | POS uses rows where F=0

---

## ⚖️ SOP vs POS

| Feature | SOP | POS |
|---------|-----|-----|
| Form | OR of AND terms | AND of OR terms |
| Based on | Minterms (F=1 rows) | Maxterms (F=0 rows) |
| Notation | Σm(...) | ΠM(...) |
| Implementation | AND gates → OR gate | OR gates → AND gate |
| Simpler when | More 1s than 0s | More 0s than 1s |

---

## ✏️ Converting Between Forms

```
F = Σm(1,3,4,6)  [3 variables, so rows 0-7]
F̄ = Σm(0,2,5,7)  [complement = remaining minterms]
F = ΠM(0,2,5,7)  [POS uses same indices as F̄'s minterms]
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** In SOP minterms, variables with value 0 are complemented. In POS maxterms, variables with value 1 are complemented.
> 🚫 **Mistake 2:** Canonical SOP ≠ minimal SOP. Canonical is the full form; K-map gives the minimal form.
> 🚫 **Mistake 3:** `Σm(1,3)` for 2 variables vs 3 variables gives different expressions — always specify number of variables.

---

## ⚡ One-Minute Recap

- Minterm: product term = 1 for one row | Maxterm: sum term = 0 for one row
- SOP = OR of minterms where F=1 | POS = AND of maxterms where F=0
- Canonical = full form | Minimal = simplified (via K-map)
- F = Σm(1,3,4,6) ↔ F = ΠM(0,2,5,7) for 3 variables

---

## 📝 Probable Exam Questions

> **5-mark:** Given truth table, write canonical SOP and POS expressions.
> **Short note:** What is the difference between a minterm and a maxterm?
> **Convert:** Express `F = Σm(0,2,5,7)` in canonical POS form.

---

---

# 3. Karnaugh Maps (K-Map)

## 💡 Intuition First

> A K-map is a **visual tool for simplifying Boolean expressions**. Instead of applying algebra rules blindly, you group adjacent 1s on a grid — each group eliminates one variable. Bigger groups = simpler expression.

**Real-world analogy:** Like finding patterns in a crossword puzzle — adjacent filled squares form groups that simplify to a single term.

---

## 📐 K-Map Layout Rules

```
CRITICAL: Adjacent cells differ by EXACTLY ONE variable (Gray code order)
Gray code: 00, 01, 11, 10  (NOT 00, 01, 10, 11)

The map WRAPS AROUND — top/bottom and left/right edges are adjacent!
```

---

## 📐 2-Variable K-Map

```
        B=0    B=1
A=0  │  m₀  │  m₁  │
A=1  │  m₂  │  m₃  │

Example: F = Σm(1,2,3)

        B=0    B=1
A=0  │   0  │   1  │
A=1  │   1  │   1  │

Groups:
  Group 1: m₁, m₃ (column B=1) → B  (A eliminated)
  Group 2: m₂, m₃ (row A=1)   → A  (B eliminated)

F = A + B
```

---

## 📐 3-Variable K-Map

```
Layout (AB on rows, C on columns):
         C=0    C=1
AB=00 │  m₀  │  m₁  │
AB=01 │  m₂  │  m₃  │
AB=11 │  m₆  │  m₇  │
AB=10 │  m₄  │  m₅  │

Note: AB order is 00,01,11,10 (Gray code — NOT 00,01,10,11!)
```

### Worked Example — 3-Variable

```
F(A,B,C) = Σm(0,1,2,3,4,5)

         C=0    C=1
AB=00 │   1  │   1  │  m₀  m₁
AB=01 │   1  │   1  │  m₂  m₃
AB=11 │   0  │   0  │  m₆  m₇
AB=10 │   1  │   1  │  m₄  m₅

Groups:
  Group 1: m₀,m₁,m₂,m₃ (top two rows) → Ā  (B,C eliminated)
  Group 2: m₀,m₁,m₄,m₅ (columns C=0,C=1 with AB=00,10)
           → B̄  (A,C eliminated)

Wait — let's re-examine:
  m₀,m₁,m₂,m₃ → A=0 for all → term = Ā
  m₀,m₁,m₄,m₅ → B=0 for all → term = B̄

F = Ā + B̄
```

---

## 📐 4-Variable K-Map

```
Layout (AB on rows, CD on columns):

         CD=00  CD=01  CD=11  CD=10
AB=00 │   m₀  │  m₁  │  m₃  │  m₂  │
AB=01 │   m₄  │  m₅  │  m₇  │  m₆  │
AB=11 │  m₁₂  │ m₁₃  │ m₁₅  │ m₁₄  │
AB=10 │   m₈  │  m₉  │ m₁₁  │ m₁₀  │
```

### Worked Example — 4-Variable

```
F(A,B,C,D) = Σm(0,1,2,3,4,5,6,7,8,9,10,11)

         CD=00  CD=01  CD=11  CD=10
AB=00 │   1  │   1  │   1  │   1  │
AB=01 │   1  │   1  │   1  │   1  │
AB=11 │   0  │   0  │   0  │   0  │
AB=10 │   1  │   1  │   1  │   1  │

Group: All 12 ones — rows AB=00,01,10 (not AB=11)
  AB=11 means A=1,B=1 → these are 0
  Remaining: when NOT (A=1 AND B=1) → B̄ + Ā

Actually: rows 00,01,10 have B=0 OR A=0
  Group top 8 (AB=00,01): Ā (A=0 for all)
  Group left 8 (AB=00,10 + CD=00,01): B̄ (B=0 for all)

F = Ā + B̄
```

### Worked Example — 4-Variable with Don't Cares

```
F(A,B,C,D) = Σm(1,3,7,11,15) + d(0,2,5)
(d = don't care — can be 0 or 1, use to make bigger groups)

         CD=00  CD=01  CD=11  CD=10
AB=00 │   d  │   1  │   1  │   d  │
AB=01 │   0  │   d  │   1  │   0  │
AB=11 │   0  │   0  │   1  │   0  │
AB=10 │   0  │   0  │   1  │   0  │

Groups (use don't cares to enlarge):
  Group 1: m₁,m₃,d₀,d₂ (top row) → Ā  (B,C,D eliminated)
  Group 2: m₃,m₇,m₁₁,m₁₅ (CD=11 column) → CD  (A,B eliminated)

F = Ā + CD
```

---

## 📏 K-Map Grouping Rules

```
✅ Groups must be powers of 2: 1, 2, 4, 8, 16
✅ Groups must be rectangular (including wrap-around)
✅ Each group should be as LARGE as possible
✅ Every 1 must be covered by at least one group
✅ Use don't cares (X) to enlarge groups if helpful
✅ Minimize number of groups (each group = one product term)

Group size → variables eliminated:
  Group of 1  → 0 variables eliminated (all 4 appear)
  Group of 2  → 1 variable eliminated
  Group of 4  → 2 variables eliminated
  Group of 8  → 3 variables eliminated
  Group of 16 → 4 variables eliminated (F = 1)
```

---

## ✏️ Reading a Group

```
To find the term for a group:
  Look at which variables are CONSTANT across all cells in the group
  If variable = 1 throughout → include it uncomplemented
  If variable = 0 throughout → include it complemented
  If variable changes → eliminate it (it's been simplified away)

Example: Group covers m₄,m₅,m₆,m₇
  m₄ = 0100, m₅ = 0101, m₆ = 0110, m₇ = 0111
  A: always 0 → Ā
  B: always 1 → B
  C: changes (0,0,1,1) → eliminated
  D: changes (0,1,0,1) → eliminated
  Term = ĀB
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** K-map column/row order is Gray code (00,01,**11**,10) — NOT binary order (00,01,10,11).
> 🚫 **Mistake 2:** Forgetting wrap-around — top row is adjacent to bottom row, left column to right column.
> 🚫 **Mistake 3:** Groups must be rectangular — L-shapes and T-shapes are NOT valid.
> 🚫 **Mistake 4:** Don't cares can be included in groups but don't HAVE to be covered.
> 🚫 **Mistake 5:** Always use the LARGEST possible groups — don't use small groups when larger ones exist.

---

## 🎯 Exam Tips

> 💡 **Always draw the K-map grid first**, fill in 1s and 0s, then identify groups.
> 💡 Start with the largest possible groups (8s, then 4s, then 2s, then 1s).
> 💡 A cell can belong to multiple groups — use it in the largest group possible.
> 💡 For 4-variable K-map: corner cells (m₀,m₂,m₈,m₁₀) form a valid group of 4!

---

## ⚡ One-Minute Recap

- K-map: visual simplification tool, group adjacent 1s
- Groups: powers of 2, rectangular, wrap-around allowed
- Larger group = fewer variables in term = simpler expression
- Gray code order: 00, 01, 11, 10 (NOT binary order)
- Don't cares: use to enlarge groups for simpler result

---

## 📝 Probable Exam Questions

> **5-mark:** Minimize `F(A,B,C,D) = Σm(0,1,2,4,5,6,8,9,12,13,14)` using a 4-variable K-map.
> **5-mark:** Simplify `F(A,B,C) = Σm(0,2,4,6)` using a 3-variable K-map.
> **Short note:** What are don't care conditions in K-maps? How are they used?
> **Draw:** Draw the 4-variable K-map layout showing all minterm positions.

---

---

# 4. Logic Gates

## 💡 Intuition First

> Logic gates are the **building blocks of all digital circuits** — like LEGO bricks for electronics. Each gate performs one Boolean operation. Combine them to build anything from a calculator to a CPU.

---

## 📐 Basic Gates — Truth Tables & Symbols

### AND Gate
```
Symbol:  A ──┐
             ├D──── F = A·B
         B ──┘

Truth Table:
A │ B │ F=A·B
──┼───┼──────
0 │ 0 │  0
0 │ 1 │  0
1 │ 0 │  0
1 │ 1 │  1    ← only 1 when BOTH inputs are 1
```

### OR Gate
```
Symbol:  A ──┐
             ├≥1─── F = A+B
         B ──┘

Truth Table:
A │ B │ F=A+B
──┼───┼──────
0 │ 0 │  0
0 │ 1 │  1
1 │ 0 │  1
1 │ 1 │  1    ← 0 only when BOTH inputs are 0
```

### NOT Gate (Inverter)
```
Symbol:  A ──▷○──── F = Ā

Truth Table:
A │ F=Ā
──┼────
0 │  1
1 │  0
```

### NAND Gate (Universal Gate)
```
Symbol:  A ──┐
             ├D○─── F = (A·B)̄ = Ā+B̄
         B ──┘

Truth Table:
A │ B │ F=(AB)̄
──┼───┼────────
0 │ 0 │   1
0 │ 1 │   1
1 │ 0 │   1
1 │ 1 │   0    ← only 0 when BOTH inputs are 1
```

### NOR Gate (Universal Gate)
```
Symbol:  A ──┐
             ├≥1○── F = (A+B)̄ = Ā·B̄
         B ──┘

Truth Table:
A │ B │ F=(A+B)̄
──┼───┼─────────
0 │ 0 │    1    ← only 1 when BOTH inputs are 0
0 │ 1 │    0
1 │ 0 │    0
1 │ 1 │    0
```

### XOR Gate
```
Symbol:  A ──┐
             ├=1─── F = A⊕B = ĀB + AB̄
         B ──┘

Truth Table:
A │ B │ F=A⊕B
──┼───┼───────
0 │ 0 │   0
0 │ 1 │   1
1 │ 0 │   1
1 │ 1 │   0    ← 1 when inputs are DIFFERENT
```

### XNOR Gate
```
F = A⊙B = AB + ĀB̄

Truth Table:
A │ B │ F=A⊙B
──┼───┼───────
0 │ 0 │   1
0 │ 1 │   0
1 │ 0 │   0
1 │ 1 │   1    ← 1 when inputs are SAME
```

---

## 🔑 Universal Gates

> **NAND and NOR are universal** — any Boolean function can be implemented using only NAND gates (or only NOR gates).

```
Implementing basic gates using only NAND:

NOT using NAND:
  A ──┬── NAND ──── Ā
      └──┘
  (connect both inputs together)

AND using NAND:
  A ──┐
      ├── NAND ──┬── NAND ──── AB
  B ──┘          └──┘
  (NAND followed by NOT)

OR using NAND:
  A ──┬── NAND ──┐
      └──┘        ├── NAND ──── A+B
  B ──┬── NAND ──┘
      └──┘
  (NOT each input, then NAND)
```

---

## ⚖️ Gate Comparison

| Gate | Symbol | Output=1 when | Universal? |
|------|--------|---------------|------------|
| AND | · | All inputs = 1 | ❌ |
| OR | + | Any input = 1 | ❌ |
| NOT | ¯ | Input = 0 | ❌ |
| NAND | (·)̄ | NOT all inputs = 1 | ✅ |
| NOR | (+)̄ | All inputs = 0 | ✅ |
| XOR | ⊕ | Odd number of 1s | ❌ |
| XNOR | ⊙ | Even number of 1s | ❌ |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** NAND output is 0 only when ALL inputs are 1 (not just one).
> 🚫 **Mistake 2:** XOR with more than 2 inputs: output = 1 when ODD number of inputs are 1.
> 🚫 **Mistake 3:** XNOR is the complement of XOR: `A⊙B = (A⊕B)̄`.
> 🚫 **Mistake 4:** AND and OR are NOT universal — you can't make a NOT gate from AND/OR alone.

---

## ⚡ One-Minute Recap

- AND: all 1s → 1 | OR: any 1 → 1 | NOT: invert
- NAND = NOT AND (universal) | NOR = NOT OR (universal)
- XOR: different inputs → 1 | XNOR: same inputs → 1
- NAND/NOR are universal — can build any circuit from them alone

---

## 📝 Probable Exam Questions

> **Short note:** Why are NAND and NOR called universal gates?
> **Draw:** Implement an AND gate using only NAND gates.
> **Truth table:** Write the truth table for a 3-input XOR gate.
> **Implement:** Realize `F = AB + C̄` using only NAND gates.

---

---

# 5. Combinational Circuits — Adders

## 💡 Intuition First

> An adder is the heart of the ALU (Arithmetic Logic Unit). It adds binary numbers just like you add decimal numbers — digit by digit, carrying over when the sum exceeds the base.

---

## 📐 Half Adder

> Adds two **single bits**. No carry input. Produces Sum and Carry out.

```
Inputs:  A, B
Outputs: Sum (S), Carry (C)

Truth Table:
A │ B │ S │ C
──┼───┼───┼───
0 │ 0 │ 0 │ 0
0 │ 1 │ 1 │ 0
1 │ 0 │ 1 │ 0
1 │ 1 │ 0 │ 1   ← 1+1 = 10 in binary (sum=0, carry=1)

Boolean expressions:
  S = A ⊕ B    (XOR)
  C = A · B    (AND)

Circuit:
  A ──┬── XOR ──── S
      │
  B ──┤
      └── AND ──── C
```

---

## 📐 Full Adder

> Adds two bits **plus a carry-in**. Used to chain multiple adders for multi-bit addition.

```
Inputs:  A, B, Cin (carry in)
Outputs: Sum (S), Cout (carry out)

Truth Table:
A │ B │Cin│ S │Cout
──┼───┼───┼───┼────
0 │ 0 │ 0 │ 0 │ 0
0 │ 0 │ 1 │ 1 │ 0
0 │ 1 │ 0 │ 1 │ 0
0 │ 1 │ 1 │ 0 │ 1
1 │ 0 │ 0 │ 1 │ 0
1 │ 0 │ 1 │ 0 │ 1
1 │ 1 │ 0 │ 0 │ 1
1 │ 1 │ 1 │ 1 │ 1

Boolean expressions:
  S    = A ⊕ B ⊕ Cin
  Cout = A·B + B·Cin + A·Cin
       = A·B + Cin·(A⊕B)

Circuit (using two Half Adders):
  A ──┐
      ├── HA₁ ──S₁──┐
  B ──┘       C₁    ├── HA₂ ──── S (final sum)
                    │       C₂──┐
              Cin ──┘            ├── OR ──── Cout
                            C₁──┘
```

---

## 🔗 4-Bit Ripple Carry Adder

```
Add A₃A₂A₁A₀ + B₃B₂B₁B₀

  A₀B₀     A₁B₁     A₂B₂     A₃B₃
   │ │       │ │       │ │       │ │
  [FA]──C₁─►[FA]──C₂─►[FA]──C₃─►[FA]──► Cout
   │         │         │         │
   S₀        S₁        S₂        S₃

Cin₀ = 0 (no initial carry)
Result: Cout S₃ S₂ S₁ S₀

Problem: Carry must "ripple" through all stages → slow for large n
Solution: Carry Lookahead Adder (CLA) — computes carries in parallel
```

---

## ⚖️ Half Adder vs Full Adder

| Feature | Half Adder | Full Adder |
|---------|------------|------------|
| Inputs | A, B | A, B, Cin |
| Outputs | S, C | S, Cout |
| Carry in | ❌ | ✅ |
| Use | First bit position | All other positions |
| Gates needed | 1 XOR + 1 AND | 2 XOR + 3 AND + 1 OR |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Half adder has NO carry input — use full adder when chaining.
> 🚫 **Mistake 2:** Sum = XOR (not AND). Carry = AND (not OR).
> 🚫 **Mistake 3:** Full adder Cout = AB + BCin + ACin — three terms, not two.

---

## ⚡ One-Minute Recap

- Half adder: S = A⊕B, C = AB (no carry in)
- Full adder: S = A⊕B⊕Cin, Cout = AB + BCin + ACin
- Full adder = two half adders + OR gate
- Ripple carry adder: chain full adders, carry propagates bit by bit

---

## 📝 Probable Exam Questions

> **5-mark:** Design a full adder. Draw the truth table, derive Boolean expressions, and draw the circuit.
> **Short note:** How is a full adder constructed from two half adders?
> **Circuit:** Draw a 4-bit ripple carry adder using full adders.

---

---

# 6. Multiplexer & Demultiplexer

## 💡 Intuition First

> **Multiplexer (MUX):** Like a TV remote — many channels (inputs), one screen (output). You select which channel to display using the channel number (select lines).
>
> **Demultiplexer (DEMUX):** The reverse — one input, many outputs. Like a post office routing one letter to one of many mailboxes.

---

## 📐 Multiplexer (MUX)

> A **2ⁿ-to-1 MUX** has 2ⁿ data inputs, n select lines, and 1 output.

### 2-to-1 MUX

```
Inputs:  I₀, I₁ (data), S (select)
Output:  Y

Truth Table:
S │ Y
──┼───
0 │ I₀   (select I₀)
1 │ I₁   (select I₁)

Boolean: Y = S̄·I₀ + S·I₁

Circuit:
  I₀ ──┐
        ├── AND ──┐
  S̄ ──┘          ├── OR ──── Y
  I₁ ──┐          │
        ├── AND ──┘
  S  ──┘
```

### 4-to-1 MUX

```
Inputs:  I₀, I₁, I₂, I₃ (data), S₁, S₀ (select)
Output:  Y

S₁│S₀│ Y
──┼──┼───
 0│ 0│ I₀
 0│ 1│ I₁
 1│ 0│ I₂
 1│ 1│ I₃

Boolean: Y = S̄₁S̄₀·I₀ + S̄₁S₀·I₁ + S₁S̄₀·I₂ + S₁S₀·I₃

Block diagram:
  I₀ ──┐
  I₁ ──┤  4-to-1
  I₂ ──┤   MUX  ──── Y
  I₃ ──┘
  S₁ S₀ (select)
```

### MUX as Universal Logic Element

```
A 2ⁿ-to-1 MUX can implement ANY function of n+1 variables!

Example: Implement F(A,B,C) using 4-to-1 MUX
  Use A,B as select lines (S₁=A, S₀=B)
  Connect C or its complement to data inputs based on truth table:

A │ B │ C │ F    Data input
──┼───┼───┼───   ──────────
0 │ 0 │ 0 │ 0 ┐
0 │ 0 │ 1 │ 0 ┘  I₀ = 0
0 │ 1 │ 0 │ 1 ┐
0 │ 1 │ 1 │ 0 ┘  I₁ = C̄
1 │ 0 │ 0 │ 0 ┐
1 │ 0 │ 1 │ 1 ┘  I₂ = C
1 │ 1 │ 0 │ 1 ┐
1 │ 1 │ 1 │ 1 ┘  I₃ = 1
```

---

## 📐 Demultiplexer (DEMUX)

> A **1-to-2ⁿ DEMUX** has 1 data input, n select lines, and 2ⁿ outputs.

### 1-to-4 DEMUX

```
Input:   D (data), S₁, S₀ (select)
Outputs: Y₀, Y₁, Y₂, Y₃

S₁│S₀│ Active Output
──┼──┼──────────────
 0│ 0│ Y₀ = D
 0│ 1│ Y₁ = D
 1│ 0│ Y₂ = D
 1│ 1│ Y₃ = D

Boolean:
  Y₀ = D·S̄₁·S̄₀
  Y₁ = D·S̄₁·S₀
  Y₂ = D·S₁·S̄₀
  Y₃ = D·S₁·S₀
```

---

## ⚖️ MUX vs DEMUX

| Feature | MUX | DEMUX |
|---------|-----|-------|
| Direction | Many → One | One → Many |
| Data inputs | 2ⁿ | 1 |
| Outputs | 1 | 2ⁿ |
| Select lines | n | n |
| Analogy | TV remote (select channel) | Post office (route letter) |
| Use | Data selection, function implementation | Data routing, decoder |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** A 4-to-1 MUX has 2 select lines (not 4). n select lines → 2ⁿ inputs.
> 🚫 **Mistake 2:** In MUX-as-logic, the select lines are the most significant variables.
> 🚫 **Mistake 3:** DEMUX routes data to ONE output at a time — all others are 0.

---

## ⚡ One-Minute Recap

- MUX: 2ⁿ inputs, n selects, 1 output — selects one input to pass through
- DEMUX: 1 input, n selects, 2ⁿ outputs — routes input to one output
- 4-to-1 MUX: 2 select lines | 8-to-1 MUX: 3 select lines
- MUX can implement any Boolean function

---

## 📝 Probable Exam Questions

> **5-mark:** Design a 4-to-1 multiplexer. Draw the truth table and circuit diagram.
> **5-mark:** Implement `F(A,B,C) = Σm(1,3,5,6)` using a 4-to-1 MUX.
> **Short note:** What is the difference between a MUX and a DEMUX?

---

---

# 7. Encoder & Decoder

## 💡 Intuition First

> **Encoder:** Converts a human-readable input (like pressing key "5" on a keyboard) into a binary code. Many inputs → fewer outputs.
>
> **Decoder:** Converts a binary code back into a specific output. Fewer inputs → many outputs. Like a 7-segment display driver.

---

## 📐 Encoder

> An **n-to-m encoder** has 2ⁿ inputs and n outputs (m = log₂(2ⁿ) = n bits).

### 4-to-2 Encoder (Priority Encoder)

```
Inputs:  I₀, I₁, I₂, I₃ (only one active at a time)
Outputs: A₁, A₀ (binary code)

Truth Table:
I₃│I₂│I₁│I₀│ A₁│A₀
──┼──┼──┼──┼───┼──
 0│ 0│ 0│ 1│  0│ 0   (I₀ active → code 00)
 0│ 0│ 1│ 0│  0│ 1   (I₁ active → code 01)
 0│ 1│ 0│ 0│  1│ 0   (I₂ active → code 10)
 1│ 0│ 0│ 0│  1│ 1   (I₃ active → code 11)

Boolean:
  A₁ = I₂ + I₃
  A₀ = I₁ + I₃
```

### 8-to-3 Encoder

```
8 inputs (I₀–I₇), 3 output bits (A₂, A₁, A₀)

A₂ = I₄ + I₅ + I₆ + I₇
A₁ = I₂ + I₃ + I₆ + I₇
A₀ = I₁ + I₃ + I₅ + I₇
```

---

## 📐 Decoder

> An **n-to-2ⁿ decoder** has n inputs and 2ⁿ outputs. Exactly ONE output is active (high) at a time.

### 2-to-4 Decoder

```
Inputs:  A₁, A₀ (binary code), Enable (E)
Outputs: Y₀, Y₁, Y₂, Y₃

Truth Table (E=1):
A₁│A₀│ Y₃│Y₂│Y₁│Y₀
──┼──┼───┼──┼──┼──
 0│ 0│  0│ 0│ 0│ 1   (Y₀ active)
 0│ 1│  0│ 0│ 1│ 0   (Y₁ active)
 1│ 0│  0│ 1│ 0│ 0   (Y₂ active)
 1│ 1│  1│ 0│ 0│ 0   (Y₃ active)

Boolean:
  Y₀ = Ā₁·Ā₀·E
  Y₁ = Ā₁·A₀·E
  Y₂ = A₁·Ā₀·E
  Y₃ = A₁·A₀·E
```

### 3-to-8 Decoder

```
3 inputs (A₂,A₁,A₀), 8 outputs (Y₀–Y₇)
Each output = one minterm of the 3 input variables

Y₀ = Ā₂Ā₁Ā₀  (minterm 0)
Y₁ = Ā₂Ā₁A₀  (minterm 1)
Y₂ = Ā₂A₁Ā₀  (minterm 2)
...
Y₇ = A₂A₁A₀  (minterm 7)

Key use: Implement any Boolean function!
  F = Σm(1,3,5) → F = Y₁ + Y₃ + Y₅
  (just OR the required decoder outputs)
```

---

## ⚖️ Encoder vs Decoder

| Feature | Encoder | Decoder |
|---------|---------|---------|
| Direction | Many → Few | Few → Many |
| Inputs | 2ⁿ (one active) | n bits |
| Outputs | n bits | 2ⁿ (one active) |
| Function | Convert to binary | Convert from binary |
| Example | Keyboard, priority encoder | 7-segment display, memory select |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** In a basic encoder, only ONE input should be active at a time. Priority encoder handles multiple active inputs.
> 🚫 **Mistake 2:** Decoder outputs are minterms — this is the key to using decoders for function implementation.
> 🚫 **Mistake 3:** A 3-to-8 decoder has 3 inputs and 8 outputs (not 3 outputs).

---

## ⚡ One-Minute Recap

- Encoder: 2ⁿ inputs → n outputs (binary code)
- Decoder: n inputs → 2ⁿ outputs (one active at a time)
- Decoder outputs = minterms → can implement any function with OR gates
- Priority encoder: handles multiple simultaneous inputs

---

## 📝 Probable Exam Questions

> **5-mark:** Design a 2-to-4 decoder with enable. Draw truth table and circuit.
> **5-mark:** Implement `F(A,B,C) = Σm(0,3,5,6)` using a 3-to-8 decoder and OR gates.
> **Short note:** What is a priority encoder? How does it differ from a basic encoder?

---

---

# 8. Flip-Flops

## 💡 Intuition First

> A flip-flop is a **1-bit memory element** — it remembers whether it's storing a 0 or a 1. Unlike combinational circuits (output depends only on current input), flip-flops are **sequential** — output depends on current input AND previous state.

**Real-world analogy:** A light switch with memory — it stays in its last position (on or off) until you explicitly change it.

---

## 📐 SR Flip-Flop (Set-Reset)

```
Inputs:  S (Set), R (Reset), Clock
Output:  Q (current state), Q̄ (complement)

Truth Table (clocked):
S │ R │ Q(next) │ Comment
──┼───┼─────────┼──────────────
0 │ 0 │  Q      │ No change (hold)
0 │ 1 │  0      │ Reset (Q=0)
1 │ 0 │  1      │ Set (Q=1)
1 │ 1 │  ?      │ INVALID (forbidden!)

Characteristic equation: Q(next) = S + R̄·Q
Constraint: S·R = 0 (both cannot be 1 simultaneously)

State diagram:
         S=1,R=0
    ┌──────────────────┐
    │                  ▼
  (Q=0)              (Q=1)
    ▲                  │
    └──────────────────┘
         S=0,R=1
    (S=0,R=0 → stay in current state)
```

---

## 📐 D Flip-Flop (Data/Delay)

```
Input:   D (data), Clock
Output:  Q

Truth Table:
D │ Q(next)
──┼─────────
0 │    0     (Q follows D)
1 │    1

Characteristic equation: Q(next) = D

Key property: Output Q = D after clock edge
              "D flip-flop delays D by one clock cycle"

State diagram:
         D=1
    ┌──────────────────┐
    │                  ▼
  (Q=0)              (Q=1)
    ▲                  │
    └──────────────────┘
         D=0
    (D=0 → stay 0, D=1 → stay 1)
```

---

## 📐 JK Flip-Flop

```
Inputs:  J (like Set), K (like Reset), Clock
Output:  Q

Truth Table:
J │ K │ Q(next) │ Comment
──┼───┼─────────┼──────────────
0 │ 0 │  Q      │ No change
0 │ 1 │  0      │ Reset
1 │ 0 │  1      │ Set
1 │ 1 │  Q̄      │ TOGGLE ← key difference from SR!

Characteristic equation: Q(next) = J·Q̄ + K̄·Q

JK flip-flop solves the SR invalid state problem:
  When J=K=1 → output TOGGLES (not invalid)
```

---

## 📐 T Flip-Flop (Toggle)

```
Input:   T (toggle), Clock
Output:  Q

Truth Table:
T │ Q(next) │ Comment
──┼─────────┼──────────────
0 │  Q      │ No change
1 │  Q̄      │ Toggle

Characteristic equation: Q(next) = T⊕Q

Key use: Counters! Each T=1 toggles the bit.
```

---

## ⚖️ Flip-Flop Comparison

| FF Type | Inputs | Invalid State | Key Feature |
|---------|--------|---------------|-------------|
| **SR** | S, R | S=R=1 | Basic set/reset |
| **D** | D | None | Stores one bit, delays by 1 clock |
| **JK** | J, K | None | Toggle when J=K=1 |
| **T** | T | None | Toggle on T=1 |

### Conversions Between Flip-Flops

```
D from JK:  J=D, K=D̄
T from JK:  J=T, K=T
JK from D:  D = J·Q̄ + K̄·Q
SR from JK: J=S, K=R (with S·R=0 constraint)
```

---

## 🔄 Flip-Flop Timing

```
Edge-triggered flip-flop:
  Changes state only at clock edge (rising or falling)

  Clock: _____|‾‾‾‾‾|_____|‾‾‾‾‾|_____
                ↑           ↑
           Rising edge  Rising edge
           (state changes here)

Setup time:  D must be stable BEFORE clock edge
Hold time:   D must be stable AFTER clock edge
Propagation: Delay from clock edge to Q changing
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** SR flip-flop: S=R=1 is FORBIDDEN. JK flip-flop: J=K=1 is TOGGLE (not forbidden).
> 🚫 **Mistake 2:** D flip-flop output = D after clock edge, not immediately.
> 🚫 **Mistake 3:** T flip-flop with T=0 holds state; T=1 toggles — it does NOT set to 1.
> 🚫 **Mistake 4:** Flip-flops are synchronous (clock-driven), not asynchronous (immediate).

---

## 🎯 Exam Tips

> 💡 **Characteristic equations** are frequently asked — memorize all four.
> 💡 JK is the most versatile — can act as SR, D, or T flip-flop.
> 💡 State diagrams show transitions between Q=0 and Q=1 based on inputs.
> 💡 T flip-flop is used in counters — each stage divides frequency by 2.

---

## ⚡ One-Minute Recap

- SR: Set/Reset, invalid when S=R=1
- D: Q(next)=D, simple 1-bit memory
- JK: like SR but J=K=1 → toggle (no invalid state)
- T: T=0 hold, T=1 toggle
- All are edge-triggered (change on clock edge)

---

## 📝 Probable Exam Questions

> **5-mark:** Draw the truth table, characteristic equation, and state diagram for a JK flip-flop.
> **Short note:** How does a JK flip-flop differ from an SR flip-flop?
> **Convert:** Design a D flip-flop using a JK flip-flop.
> **Trace:** Given a sequence of J,K inputs and initial Q=0, trace the output for 5 clock cycles.

---

---

# 9. Counters

## 💡 Intuition First

> A counter is a sequential circuit that counts clock pulses. Like an odometer in a car — each pulse increments the count. Counters are built from flip-flops, where each flip-flop represents one bit.

---

## 📐 Asynchronous (Ripple) Counter

> Each flip-flop is triggered by the output of the previous one — the clock "ripples" through. Simple but slow (propagation delay accumulates).

### 3-Bit Ripple Up Counter (using T flip-flops with T=1)

```
Clock ──► FF₀(T=1) ──Q₀──► FF₁(T=1) ──Q₁──► FF₂(T=1) ──Q₂

Each FF toggles when its input goes from 1→0 (falling edge)

Timing diagram:
Clock: ‾|_|‾|_|‾|_|‾|_|‾|_|‾|_|‾|_|‾|_|
Q₀:    ‾‾|__|‾‾|__|‾‾|__|‾‾|__|  (toggles every clock)
Q₁:    ‾‾‾‾‾‾|____|‾‾‾‾‾‾|____  (toggles every 2 clocks)
Q₂:    ‾‾‾‾‾‾‾‾‾‾‾‾|________|   (toggles every 4 clocks)

Count sequence (Q₂Q₁Q₀):
000 → 001 → 010 → 011 → 100 → 101 → 110 → 111 → 000
 0  →  1  →  2  →  3  →  4  →  5  →  6  →  7  → 0 (wraps)
```

---

## 📐 Synchronous Counter

> All flip-flops are triggered by the SAME clock simultaneously. Faster than ripple counter (no propagation delay accumulation).

### 3-Bit Synchronous Up Counter

```
Using JK flip-flops:

FF₀: J₀=K₀=1 (always toggles)
FF₁: J₁=K₁=Q₀ (toggles when Q₀=1)
FF₂: J₂=K₂=Q₀·Q₁ (toggles when Q₀=Q₁=1)

Count sequence: 000→001→010→011→100→101→110→111→000
```

---

## 📐 MOD-N Counter

> A counter that counts from 0 to N-1, then resets to 0.

```
MOD-6 counter (counts 0 to 5):
  Normal 3-bit counter counts 0-7
  When count reaches 6 (110):
    Detect 110 using NAND gate: Q₂·Q₁ = 1
    Use this to RESET all flip-flops to 0

MOD-10 (Decade counter):
  Counts 0-9, resets on 10 (1010)
  Detect 1010: Q₃·Q₁ = 1 → reset

Modulus = number of states in the count sequence
  3-bit counter: MOD-8
  4-bit counter: MOD-16
  n-bit counter: MOD-2ⁿ
```

---

## 📐 Up/Down Counter

```
Direction control input: UP/DOWN̄

UP=1:   Count up   (000→001→010→...→111→000)
UP=0:   Count down (111→110→101→...→000→111)

JK equations for up/down counter:
  J₀=K₀=1
  J₁=K₁= UP·Q₀ + DOWN̄·Q̄₀
  J₂=K₂= UP·Q₁·Q₀ + DOWN̄·Q̄₁·Q̄₀
```

---

## ⚖️ Ripple vs Synchronous Counter

| Feature | Ripple (Async) | Synchronous |
|---------|----------------|-------------|
| Clock | Cascaded (ripples) | Common clock |
| Speed | Slow (delay accumulates) | Fast |
| Complexity | Simple | More complex |
| Glitches | Yes (intermediate states) | No |
| Use | Low-speed, simple | High-speed, reliable |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Ripple counter: each FF triggered by PREVIOUS FF's output, not the main clock.
> 🚫 **Mistake 2:** MOD-N counter: reset happens WHEN count reaches N, not N-1.
> 🚫 **Mistake 3:** A 3-bit counter has 8 states (0-7), not 7 states.

---

## ⚡ One-Minute Recap

- Ripple counter: cascaded FFs, simple, slow, glitches possible
- Synchronous counter: common clock, fast, no glitches
- MOD-N: counts 0 to N-1, resets on N
- T flip-flop with T=1 divides clock frequency by 2 per stage

---

## 📝 Probable Exam Questions

> **5-mark:** Design a 3-bit synchronous up counter using JK flip-flops. Show the state table and circuit.
> **Short note:** What is the difference between a ripple counter and a synchronous counter?
> **Design:** Design a MOD-6 counter. Show how the reset is implemented.
> **Trace:** Trace the output of a 3-bit ripple counter for 10 clock pulses starting from 000.

---

---

# 10. Registers

## 💡 Intuition First

> A register is a **group of flip-flops** that stores multiple bits together — like a row of memory cells. A 4-bit register stores a 4-bit binary number. Registers are the fastest storage in a computer (inside the CPU).

---

## 📐 Types of Registers

### 1. Parallel (Buffer) Register

```
Stores n bits simultaneously. All bits loaded at once on clock edge.

4-bit parallel register:
  D₃ D₂ D₁ D₀ (data inputs)
   │  │  │  │
  [D][D][D][D]  ← 4 D flip-flops, common clock
   │  │  │  │
  Q₃ Q₂ Q₁ Q₀ (stored output)

On clock edge: Q₃Q₂Q₁Q₀ = D₃D₂D₁D₀
```

### 2. Serial-In Serial-Out (SISO) Shift Register

```
Data enters one bit at a time, exits one bit at a time.

  Data_in ──► [D₀] ──Q₀──► [D₁] ──Q₁──► [D₂] ──Q₂──► [D₃] ──► Data_out
               ↑             ↑             ↑             ↑
              CLK           CLK           CLK           CLK

Shift operation: each clock pulse shifts all bits one position right
  Initial:  Q₃Q₂Q₁Q₀ = 0000
  Input 1:  Q₃Q₂Q₁Q₀ = 0001
  Input 0:  Q₃Q₂Q₁Q₀ = 0010
  Input 1:  Q₃Q₂Q₁Q₀ = 0101
  Input 1:  Q₃Q₂Q₁Q₀ = 1011
```

### 3. Serial-In Parallel-Out (SIPO)

```
Data enters serially, all bits available simultaneously as output.
Used for: Serial-to-parallel conversion (e.g., receiving serial data)
```

### 4. Parallel-In Serial-Out (PISO)

```
All bits loaded simultaneously, shifted out one at a time.
Used for: Parallel-to-serial conversion (e.g., transmitting data serially)
```

### 5. Universal Shift Register

```
Can perform all four operations:
  - Parallel load
  - Shift right
  - Shift left
  - Hold (no change)

Controlled by 2 mode select bits (S₁, S₀):
S₁│S₀│ Operation
──┼──┼──────────
 0│ 0│ Hold
 0│ 1│ Shift right
 1│ 0│ Shift left
 1│ 1│ Parallel load
```

---

## 📐 Shift Register Applications

| Application | Register Type | Description |
|-------------|---------------|-------------|
| Serial communication | PISO | Convert parallel data to serial for transmission |
| Data reception | SIPO | Convert received serial data to parallel |
| Delay line | SISO | Delay signal by n clock cycles |
| Ring counter | SISO (circular) | Circulate a single 1 bit |
| Johnson counter | SISO (feedback) | Twisted ring counter |

---

## 🔄 Ring Counter vs Johnson Counter

```
Ring Counter (4-bit):
  Initial: 1000
  After 1: 0100
  After 2: 0010
  After 3: 0001
  After 4: 1000 (repeats)
  MOD-4 counter, only one 1 circulates

Johnson Counter (4-bit):
  Initial: 0000
  After 1: 1000  (shift in 1 from Q̄₃)
  After 2: 1100
  After 3: 1110
  After 4: 1111
  After 5: 0111  (shift in 0 from Q̄₃)
  After 6: 0011
  After 7: 0001
  After 8: 0000 (repeats)
  MOD-8 counter (2n states for n flip-flops)
```

---

## ⚖️ Register Types Summary

| Type | Input | Output | Use |
|------|-------|--------|-----|
| Parallel | Parallel | Parallel | CPU registers, fast storage |
| SISO | Serial | Serial | Delay, pipeline |
| SIPO | Serial | Parallel | Serial-to-parallel conversion |
| PISO | Parallel | Serial | Parallel-to-serial conversion |
| Universal | Both | Both | Flexible, general purpose |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Shift register shifts data in the direction of the chain — right shift moves data from D₀ toward D₃.
> 🚫 **Mistake 2:** Ring counter: MOD-n (n = number of bits). Johnson counter: MOD-2n.
> 🚫 **Mistake 3:** A register stores data — it doesn't process it. Processing is done by the ALU.

---

## ⚡ One-Minute Recap

- Register: group of flip-flops storing multiple bits
- Parallel: load/read all bits at once
- Shift register: bits move one position per clock
- SISO: serial in/out | SIPO: serial in, parallel out | PISO: parallel in, serial out
- Ring counter: MOD-n | Johnson counter: MOD-2n

---

## 📝 Probable Exam Questions

> **5-mark:** Explain the operation of a 4-bit SIPO shift register with a timing diagram.
> **Short note:** What is the difference between a ring counter and a Johnson counter?
> **Design:** Design a 4-bit universal shift register. Show the mode control table.
> **Trace:** Trace the output of a 4-bit ring counter for 6 clock pulses starting from 1000.

---

---

# 🏁 Master Quick Revision Sheet — Digital Logic Design

## ⚡ Boolean Laws Cheat Sheet

```
Identity:      A+0=A    A·1=A    A+1=1    A·0=0
Complement:    A+Ā=1    A·Ā=0    Ā̄=A
Idempotent:    A+A=A    A·A=A
Absorption:    A+AB=A   A(A+B)=A
De Morgan's:   (A+B)̄=Ā·B̄    (A·B)̄=Ā+B̄
Distributive:  A(B+C)=AB+AC    A+(BC)=(A+B)(A+C)
XOR:           A⊕A=0    A⊕0=A    A⊕1=Ā    A⊕B=B⊕A
```

## 🔑 Key Facts to Remember

| Fact | Detail |
|------|--------|
| K-map order | Gray code: 00,01,**11**,10 (NOT binary) |
| K-map groups | Powers of 2 only: 1,2,4,8,16 |
| K-map wrap | Top↔Bottom, Left↔Right are adjacent |
| Universal gates | NAND and NOR only |
| Half adder | S=A⊕B, C=AB (no carry in) |
| Full adder | S=A⊕B⊕Cin, Cout=AB+BCin+ACin |
| SR invalid | S=R=1 is forbidden |
| JK toggle | J=K=1 → toggle (not invalid) |
| D flip-flop | Q(next)=D (simplest) |
| T flip-flop | Q(next)=T⊕Q (toggle on T=1) |
| Ring counter | MOD-n (n = bits) |
| Johnson counter | MOD-2n (n = bits) |
| MUX inputs | 2ⁿ data inputs, n select lines |
| Decoder outputs | Each output = one minterm |

## 🧠 Memory Tricks

- **De Morgan's:** "**Break the bar, change the sign**" → (A+B)̄ = Ā·B̄
- **K-map order:** "**Go Gray**" → 00,01,11,10 (adjacent cells differ by 1 bit)
- **Flip-flop types:** "**S**et/**R**eset, **D**elay, **J**ump/**K**ill, **T**oggle"
- **Full adder from half adders:** "**Two HAs + one OR = FA**"
- **Universal gates:** "**NAND and NOR are the universal donors**"
- **MUX vs DEMUX:** "**MUX = Many to one** | **DEMUX = one to Many**"

## 🎯 Top 10 Most Probable Exam Questions

1. Simplify Boolean expression using Boolean algebra (show each step)
2. Minimize function using 3-variable or 4-variable K-map
3. Design full adder — truth table, expressions, circuit
4. Draw truth table and circuit for 4-to-1 MUX
5. Design 2-to-4 decoder with enable
6. JK flip-flop — truth table, characteristic equation, state diagram
7. Compare SR, D, JK, T flip-flops in a table
8. Design 3-bit synchronous counter
9. Implement Boolean function using decoder + OR gates
10. Trace shift register operation for given input sequence

## 📊 Flip-Flop Quick Reference

```
┌──────┬──────────┬──────────────────────────┬──────────────┐
│  FF  │  Inputs  │  Characteristic Eq.      │  Special     │
├──────┼──────────┼──────────────────────────┼──────────────┤
│  SR  │  S, R    │  Q+ = S + R̄Q (SR=0)     │  S=R=1 invalid│
│  D   │  D       │  Q+ = D                  │  Simplest    │
│  JK  │  J, K    │  Q+ = JQ̄ + K̄Q           │  J=K=1→toggle│
│  T   │  T       │  Q+ = T⊕Q               │  T=1→toggle  │
└──────┴──────────┴──────────────────────────┴──────────────┘
```

---

> 📌 **End of Subject 05: Digital Logic Design**
>
> Next: **Subject 06 — Software Engineering** →

---

*Handbook generated for MSc Admission Preparation | JUST-Style Exam Focus*
*Version 1.0 | Digital Logic Design*
