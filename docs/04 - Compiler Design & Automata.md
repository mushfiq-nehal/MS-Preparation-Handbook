# 📘 MSc Admission Prep — Subject 04: Compiler Design & Automata
### 🎯 JUST-Style Exam Handbook | Fast Revision Edition

> **Goal:** Visual, exam-focused revision of automata theory and compiler design. Every topic includes intuition, state diagrams, derivation traces, and exam tips.

---

## 📋 Table of Contents

| # | Topic | Tier |
|---|-------|------|
| 1 | [DFA vs NFA](#1-dfa-vs-nfa) | 🔴 Must Master |
| 2 | [Regular Expressions & Regex to NFA](#2-regular-expressions--regex-to-nfa) | 🔴 Must Master |
| 3 | [DFA Minimization](#3-dfa-minimization) | 🔴 Must Master |
| 4 | [Context-Free Grammars (CFG)](#4-context-free-grammars-cfg) | 🔴 Must Master |
| 5 | [Parse Trees & Syntax Trees](#5-parse-trees--syntax-trees) | 🔴 Must Master |
| 6 | [FIRST and FOLLOW Sets](#6-first-and-follow-sets) | 🔴 Must Master |
| 7 | [Left Recursion & Left Factoring](#7-left-recursion--left-factoring) | 🔴 Must Master |
| 8 | [Phases of a Compiler](#8-phases-of-a-compiler) | 🔴 Must Master |
| 9 | [Lexical Analysis](#9-lexical-analysis) | 🔴 Must Master |
| 10 | [Parsing](#10-parsing) | 🔴 Must Master |
| 11 | [Code Generation](#11-code-generation) | 🔴 Must Master |

---

---

# 1. DFA vs NFA

## 💡 Intuition First

> A **DFA** (Deterministic Finite Automaton) is like a **GPS with one fixed route** — at every intersection, there is exactly one road to take. No ambiguity.
>
> An **NFA** (Nondeterministic Finite Automaton) is like a **GPS that can magically explore all routes simultaneously** — at each step, it can take multiple paths at once, and if ANY path leads to the destination, it accepts.

**Real-world analogy:**
- DFA = A vending machine — each button press leads to exactly one state.
- NFA = A chess computer — it explores all possible moves simultaneously.

**Why it matters:** DFA/NFA are the foundation of lexical analysis (tokenizers), pattern matching (regex), and formal language theory.

---

## 📐 Formal Definitions

### DFA — Deterministic Finite Automaton

```
A DFA is a 5-tuple: M = (Q, Σ, δ, q₀, F)

Q  = finite set of states
Σ  = input alphabet
δ  = transition function: Q × Σ → Q  (exactly ONE next state)
q₀ = start state (q₀ ∈ Q)
F  = set of accept/final states (F ⊆ Q)

Key property: δ(q, a) gives EXACTLY ONE state
              Every state must have a transition for EVERY symbol
```

### NFA — Nondeterministic Finite Automaton

```
An NFA is a 5-tuple: M = (Q, Σ, δ, q₀, F)

Same structure BUT:
δ  = transition function: Q × (Σ ∪ {ε}) → 2^Q  (set of states!)

Key differences from DFA:
  1. δ can return MULTIPLE states (or empty set)
  2. ε-transitions allowed (move without consuming input)
  3. Missing transitions are allowed (implicit dead state)
```

---

## 🔄 DFA Example — Strings ending in "ab"

```
Language: L = {w ∈ {a,b}* | w ends with "ab"}

States: q0 (start), q1 (seen 'a'), q2 (seen 'ab' = accept)

Transition diagram:
         a           b
    ┌────────────────────────────────┐
    │                                │
    ▼    a           b               │
  →(q0)────►(q1)────►((q2))         │
    ▲         │                      │
    │    a    │ a                    │
    └─────────┘                      │
         b                           │
    (q0)──────────────────────────►(q0)

Transition table:
State │  a  │  b
──────┼─────┼─────
→ q0  │ q1  │ q0
  q1  │ q1  │ q2
 *q2  │ q1  │ q0

(→ = start state, * = accept state)

Trace "aab":
  q0 →(a)→ q1 →(a)→ q1 →(b)→ q2 ✅ ACCEPT

Trace "aba":
  q0 →(a)→ q1 →(b)→ q2 →(a)→ q1 ❌ REJECT (not in F)
```

---

## 🔄 NFA Example — Strings containing "ab"

```
Language: L = {w | w contains "ab" as substring}

States: q0 (start), q1 (seen 'a'), q2 (seen 'ab' = accept)

NFA transition diagram:
         a,b
    ┌─────────┐
    │         │
    ▼    a    │    b
  →(q0)────►(q1)────►((q2))
                        │
                       a,b (stay in q2)
                        └──────────────┘

Transition table:
State │  a     │  b
──────┼────────┼──────
→ q0  │ {q0,q1}│ {q0}
  q1  │ {}     │ {q2}
 *q2  │ {q2}   │ {q2}

Trace "aab" (NFA explores all paths):
  Start: {q0}
  Read 'a': {q0, q1}  (q0→q0 on a, q0→q1 on a)
  Read 'a': {q0, q1}  (q0→q0, q0→q1, q1→{} dead)
  Read 'b': {q0, q2}  (q0→q0, q1→q2)
  q2 ∈ F → ACCEPT ✅
```

---

## ⚖️ DFA vs NFA — Master Comparison

| Feature | DFA | NFA |
|---------|-----|-----|
| Transitions | Exactly 1 per (state, symbol) | 0, 1, or many |
| ε-transitions | ❌ Not allowed | ✅ Allowed |
| Dead states | Must be explicit | Implicit (missing = dead) |
| Computation | Single path | Multiple paths simultaneously |
| Acceptance | Reach accept state | ANY path reaches accept state |
| Equivalence | Same expressive power | Same expressive power |
| Conversion | — | NFA → DFA (subset construction) |
| States after conversion | n states | Up to 2ⁿ states |
| Implementation | Easier | Harder |

> 🔑 **Key theorem:** Every NFA can be converted to an equivalent DFA (subset construction algorithm). They recognize the same class of languages — **Regular Languages**.

---

## 🔄 NFA to DFA Conversion (Subset Construction)

```
NFA:
States: {q0, q1, q2}
Alphabet: {a, b}
Start: q0, Accept: {q2}

NFA transitions:
  q0 on a → {q0, q1}
  q0 on b → {q0}
  q1 on b → {q2}
  q2 on a → {q2}
  q2 on b → {q2}

DFA states = subsets of NFA states:

DFA State │  a        │  b
──────────┼───────────┼──────────
→{q0}     │ {q0,q1}   │ {q0}
 {q0,q1}  │ {q0,q1}   │ {q0,q2}
 {q0,q2}* │ {q0,q1,q2}│ {q0,q2}
*{q0,q1,q2}│{q0,q1,q2}│{q0,q2}

(* = contains q2, so it's an accept state)
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** NFA and DFA have the **same expressive power** — both recognize regular languages only.
> 🚫 **Mistake 2:** In DFA, every state must have a transition for EVERY symbol. Missing transitions → add dead/trap state.
> 🚫 **Mistake 3:** NFA accepts if ANY computation path reaches an accept state — not all paths need to accept.
> 🚫 **Mistake 4:** ε-closure must be computed before subset construction.

---

## 🎯 Exam Tips

> 💡 **Draw the state diagram** — examiners want to see the visual automaton.
> 💡 Always label: → for start state, double circle for accept state.
> 💡 For NFA→DFA: start with ε-closure of start state, then compute transitions for each subset.
> 💡 DFA has at most 2ⁿ states after conversion from n-state NFA.

---

## ⚡ One-Minute Recap

- DFA: deterministic, exactly 1 transition per (state, symbol), no ε
- NFA: nondeterministic, 0+ transitions, ε allowed
- Both recognize regular languages (same power)
- NFA → DFA via subset construction (up to 2ⁿ states)
- Acceptance: DFA = single path to accept | NFA = any path to accept

---

## 📝 Probable Exam Questions

> **5-mark:** Design a DFA that accepts all strings over {a,b} that end with "ab". Draw the state diagram and transition table.
> **5-mark:** Convert the given NFA to an equivalent DFA using subset construction.
> **Short note:** Compare DFA and NFA. Are they equivalent in power?
> **Trace:** Trace the string "aabb" on the given DFA/NFA. Does it accept?

---

---

# 2. Regular Expressions & Regex to NFA

## 💡 Intuition First

> A **regular expression** is a compact notation for describing a pattern. Like a search filter — `a*b` means "zero or more a's followed by one b." Under the hood, every regex compiles to an NFA (Thompson's construction), which can then become a DFA.

**Real-world analogy:** Regex is like a recipe description ("one or more eggs, optional cheese") — the NFA is the actual cooking process that follows the recipe.

---

## 📐 Regular Expression Operators

| Operator | Symbol | Meaning | Example |
|----------|--------|---------|---------|
| **Concatenation** | (implicit) | One after another | `ab` = a then b |
| **Union/Alternation** | `\|` | Either one | `a\|b` = a or b |
| **Kleene Star** | `*` | Zero or more | `a*` = ε, a, aa, aaa... |
| **Plus** | `+` | One or more | `a+` = a, aa, aaa... |
| **Optional** | `?` | Zero or one | `a?` = ε or a |
| **Grouping** | `()` | Group subexpressions | `(ab)*` |

### Operator Precedence (high to low)

```
1. * (Kleene star) — highest
2. Concatenation
3. | (union) — lowest

So: a|bc* = a | (b(c*))   NOT (a|b)(c*)
```

---

## 📐 Regular Expression Examples

```
Language                          Regex
─────────────────────────────────────────────────────
Strings over {a,b}                (a|b)*
Strings starting with 'a'         a(a|b)*
Strings ending with 'b'           (a|b)*b
Strings containing "ab"           (a|b)*ab(a|b)*
Strings with even number of a's   (b*ab*ab*)*b*
Binary strings divisible by 2     (0|1)*0
Identifiers (letter then alnum*)  [a-z][a-z0-9]*
```

---

## 🔄 Thompson's Construction: Regex → NFA

> Build NFA from regex using basic building blocks. Each operator has a standard NFA fragment.

### Base Cases

```
NFA for single symbol 'a':
  →(i) ──a──► ((f))

NFA for ε:
  →(i) ──ε──► ((f))
```

### Union: r₁ | r₂

```
         ε ──► [NFA for r₁] ──ε──►
→(new_i)                            ((new_f))
         ε ──► [NFA for r₂] ──ε──►
```

### Concatenation: r₁r₂

```
→[NFA for r₁]──ε──►[NFA for r₂]──►((f))
  (merge: r₁'s accept becomes r₂'s start via ε)
```

### Kleene Star: r*

```
         ┌──────────ε──────────┐
         │                     │
→(new_i)─┤ε──►[NFA for r]──ε──►(new_f)
         │                     │
         └──────────ε──────────┘
         (ε from new_i to new_f for zero repetitions)
```

---

## ✏️ Worked Example: Regex `(a|b)*abb` → NFA

```
Step 1: Build NFA for (a|b)*
  - NFA for 'a': q0 →a→ q1
  - NFA for 'b': q2 →b→ q3
  - Union a|b: q4 →ε→ q0, q4 →ε→ q2, q1 →ε→ q5, q3 →ε→ q5
  - Star (a|b)*: q6 →ε→ q4, q5 →ε→ q4, q6 →ε→ q7, q5 →ε→ q7

Step 2: Concatenate with 'a': q7 →a→ q8
Step 3: Concatenate with 'b': q8 →b→ q9
Step 4: Concatenate with 'b': q9 →b→ q10 (accept)

Final NFA has ~11 states with ε-transitions.
```

---

## ⚖️ Regular Languages — Closure Properties

| Operation | Regular? |
|-----------|----------|
| Union | ✅ Yes |
| Concatenation | ✅ Yes |
| Kleene Star | ✅ Yes |
| Complement | ✅ Yes |
| Intersection | ✅ Yes |
| Reversal | ✅ Yes |

> 🔑 **Regular languages are closed under all these operations.**

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** `a*` includes ε (empty string). `a+` does NOT include ε.
> 🚫 **Mistake 2:** Operator precedence: `*` > concatenation > `|`. Always parenthesize when unsure.
> 🚫 **Mistake 3:** Not all languages are regular. `aⁿbⁿ` (equal a's and b's) is NOT regular — needs a stack (CFG).

---

## ⚡ One-Minute Recap

- Regex operators: `*` (zero+), `+` (one+), `?` (zero/one), `|` (union), concat
- Precedence: `*` > concat > `|`
- Thompson's construction: regex → NFA using ε-transitions
- Every regex → NFA → DFA (all equivalent for regular languages)

---

## 📝 Probable Exam Questions

> **5-mark:** Write a regular expression for strings over {0,1} that contain at least two consecutive 1s. Build the NFA.
> **Short note:** What is Thompson's construction? Explain with an example.
> **Design:** Write regex for valid identifiers (start with letter, followed by letters/digits).

---

---

# 3. DFA Minimization

## 💡 Intuition First

> A DFA might have redundant states that behave identically. Minimization removes these duplicates to get the **smallest possible DFA** for a language — like simplifying a fraction to its lowest terms.

**Why it matters:** Minimized DFAs are more efficient for implementation. Exam questions often ask you to minimize a given DFA.

---

## 📐 Minimization Algorithm (Table-Filling / Myhill-Nerode)

```
Goal: Find pairs of states that are DISTINGUISHABLE,
      then merge all INDISTINGUISHABLE pairs.

Two states p, q are DISTINGUISHABLE if:
  ∃ string w such that exactly one of δ(p,w) and δ(q,w) is in F

Algorithm:
1. Remove unreachable states
2. Create a table of all pairs (p, q) where p < q
3. Mark pairs where one is accept and other is not (base case)
4. Repeat: mark (p,q) if ∃ symbol a such that (δ(p,a), δ(q,a)) is marked
5. Unmarked pairs = equivalent states → merge them
```

---

## ✏️ Worked Example

```
DFA:
States: {A, B, C, D, E, F}
Alphabet: {0, 1}
Start: A
Accept: {C, D, E}

Transition table:
State │  0  │  1
──────┼─────┼─────
→ A   │  B  │  C
  B   │  A  │  D
 *C   │  E  │  F
 *D   │  E  │  F
 *E   │  E  │  F
  F   │  F  │  F

Step 1: No unreachable states.

Step 2: Create pairs table (upper triangle):
        B  C  D  E  F
    A   _  _  _  _  _
    B      _  _  _  _
    C         _  _  _
    D            _  _
    E               _

Step 3: Mark pairs where one is accept, other is not:
  Accept = {C,D,E}, Non-accept = {A,B,F}
  Mark: (A,C),(A,D),(A,E),(B,C),(B,D),(B,E),(C,F),(D,F),(E,F)

        B  C  D  E  F
    A   _  ✗  ✗  ✗  _
    B      ✗  ✗  ✗  _
    C         _  _  ✗
    D            _  ✗
    E               ✗

Step 4: Iterate — mark (p,q) if δ(p,a) and δ(q,a) are marked:

Check (A,B): δ(A,0)=B, δ(B,0)=A → (A,B) unmarked
             δ(A,1)=C, δ(B,1)=D → (C,D) unmarked → don't mark (A,B)

Check (C,D): δ(C,0)=E, δ(D,0)=E → (E,E) same → ok
             δ(C,1)=F, δ(D,1)=F → (F,F) same → ok
             → (C,D) UNMARKED → C and D are equivalent!

Check (C,E): δ(C,0)=E, δ(E,0)=E → same
             δ(C,1)=F, δ(E,1)=F → same
             → (C,E) UNMARKED → C and E are equivalent!

Check (D,E): Similarly → UNMARKED → D and E equivalent!

Check (A,F): δ(A,0)=B, δ(F,0)=F → (B,F) unmarked?
             δ(A,1)=C, δ(F,1)=F → (C,F) is MARKED → mark (A,F)!

Check (B,F): δ(B,0)=A, δ(F,0)=F → (A,F) now marked → mark (B,F)!

Final unmarked pairs: (A,B), (C,D), (C,E), (D,E)

Equivalence classes:
  {A, B} → merge into one state (call it AB)
  {C, D, E} → merge into one state (call it CDE)
  {F} → stays as F

Minimized DFA:
State │  0   │  1
──────┼──────┼──────
→ AB  │  AB  │  CDE
*CDE  │  CDE │  F
  F   │  F   │  F

Only 3 states! (down from 6)
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Forgetting to remove unreachable states first.
> 🚫 **Mistake 2:** The base case marks (accept, non-accept) pairs — not just accept states.
> 🚫 **Mistake 3:** Minimization applies to DFAs only — not directly to NFAs.
> 🚫 **Mistake 4:** Two states are equivalent only if ALL their transitions lead to equivalent states.

---

## ⚡ One-Minute Recap

- Minimization: find and merge indistinguishable states
- Base case: mark (accept, non-accept) pairs
- Iterate: mark (p,q) if any transition leads to a marked pair
- Unmarked pairs → equivalent → merge
- Result: smallest DFA for the language

---

## 📝 Probable Exam Questions

> **5-mark:** Minimize the given DFA using the table-filling algorithm. Show all steps.
> **Short note:** What are distinguishable states? How are they identified?
> **Conceptual:** Why is DFA minimization useful?

---

---

# 4. Context-Free Grammars (CFG)

## 💡 Intuition First

> A **CFG** is a set of rules for generating strings. Like grammar rules in English: "A sentence = noun phrase + verb phrase." You start with a symbol and keep replacing it using rules until you get a string of terminals.

**Real-world analogy:** A recipe book — start with "Meal", expand to "Main + Side + Dessert", keep expanding until you have actual ingredients (terminals).

**Why it matters:** CFGs describe programming language syntax. Parsers use CFGs to check if code is syntactically valid.

---

## 📐 Formal Definition

```
A CFG is a 4-tuple: G = (V, T, P, S)

V = set of variables (non-terminals)    e.g., {S, A, B}
T = set of terminals                    e.g., {a, b, (, )}
P = set of production rules             e.g., S → aSb | ε
S = start symbol                        e.g., S

Production rule format: A → α
  where A ∈ V and α ∈ (V ∪ T)*
```

---

## 🔄 Derivations

> A **derivation** is the process of applying production rules to generate a string.

```
Grammar: S → aSb | ε

Derive "aabb":

Leftmost derivation (always expand leftmost non-terminal):
  S ⟹ aSb ⟹ aaSbb ⟹ aaεbb ⟹ aabb ✅

Rightmost derivation (always expand rightmost non-terminal):
  S ⟹ aSb ⟹ aaSbb ⟹ aaεbb ⟹ aabb ✅
  (same result here, but order of expansion differs)
```

### Types of Derivation

| Type | Rule | Used In |
|------|------|---------|
| **Leftmost** | Expand leftmost non-terminal first | Top-down parsing |
| **Rightmost** | Expand rightmost non-terminal first | Bottom-up parsing |

---

## 📐 CFG Examples

```
1. Balanced parentheses:
   S → (S) | SS | ε

   Derive "(())":
   S ⟹ (S) ⟹ ((S)) ⟹ (()) ✅

2. Arithmetic expressions:
   E → E + E | E * E | (E) | id

3. Simple programming language:
   stmt → if expr then stmt
         | if expr then stmt else stmt
         | while expr do stmt
         | id := expr

4. aⁿbⁿ (equal a's and b's — NOT regular!):
   S → aSb | ε
   Generates: ε, ab, aabb, aaabbb, ...
```

---

## 🌳 Ambiguous Grammars

> A grammar is **ambiguous** if a string has more than one parse tree (or more than one leftmost derivation).

```
Grammar: E → E + E | E * E | id

String: id + id * id

Parse tree 1 (+ first):        Parse tree 2 (* first):
       E                               E
      /|\                             /|\
     E + E                           E * E
     |   |\ \                       /|   |
    id   E * E                     E + E  id
         |   |                     |   |
        id  id                    id  id

Two different trees → AMBIGUOUS!

Fix: Use precedence rules in grammar:
  E → E + T | T
  T → T * F | F
  F → (E) | id
```

---

## ⚖️ Regular Grammar vs CFG vs CSG

| Type | Grammar | Automaton | Example Language |
|------|---------|-----------|-----------------|
| Regular | Type 3 | DFA/NFA | a*b, identifiers |
| Context-Free | Type 2 | PDA | aⁿbⁿ, balanced parens |
| Context-Sensitive | Type 1 | LBA | aⁿbⁿcⁿ |
| Unrestricted | Type 0 | Turing Machine | Any computable |

> 🔑 **Chomsky Hierarchy:** Type 3 ⊂ Type 2 ⊂ Type 1 ⊂ Type 0

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** `aⁿbⁿ` is NOT regular — it requires a stack (CFG/PDA).
> 🚫 **Mistake 2:** Ambiguity is a property of the grammar, not the language. A language can have multiple grammars, some ambiguous, some not.
> 🚫 **Mistake 3:** ε (epsilon) is the empty string — it's a valid terminal in derivations.
> 🚫 **Mistake 4:** Leftmost and rightmost derivations produce the same string but different derivation sequences.

---

## ⚡ One-Minute Recap

- CFG: variables, terminals, productions, start symbol
- Derivation: apply rules to generate strings
- Leftmost: expand leftmost non-terminal | Rightmost: expand rightmost
- Ambiguous: one string → multiple parse trees
- CFG recognizes context-free languages (more powerful than regular)

---

## 📝 Probable Exam Questions

> **5-mark:** Write a CFG for the language {aⁿbⁿ | n ≥ 1}. Show derivation of "aaabbb".
> **5-mark:** Show that the grammar E → E+E | E*E | id is ambiguous for "id+id*id".
> **Short note:** What is the Chomsky hierarchy? Where do CFGs fit?
> **Derive:** Using the given grammar, show leftmost and rightmost derivation of a given string.

---

---

# 5. Parse Trees & Syntax Trees

## 💡 Intuition First

> A **parse tree** is the visual proof that a string belongs to a grammar. It shows exactly which rules were applied and in what order. A **syntax tree** (abstract syntax tree / AST) strips away the grammar details and keeps only the semantic structure.

**Real-world analogy:** Parse tree = full sentence diagram in English class (every word labeled). AST = the meaning extracted (subject, verb, object).

---

## 🌳 Parse Tree

> A parse tree for string w in grammar G is a tree where:
> - Root = start symbol S
> - Internal nodes = non-terminals
> - Leaves = terminals (read left to right = w)
> - Each internal node's children = right side of a production rule

```
Grammar:
  E → E + T | T
  T → T * F | F
  F → (E) | id

Parse tree for "id + id * id":

              E
             /|\
            E + T
            |   |\
            T   T * F
            |   |   |
            F   F   id
            |   |
            id  id

Reading leaves left to right: id + id * id ✅
```

---

## 🌲 Abstract Syntax Tree (AST)

> AST removes grammar artifacts (like intermediate non-terminals) and keeps only the essential structure.

```
Parse tree for "id + id * id":     AST for "id + id * id":

        E                                  +
       /|\                                / \
      E + T                             id   *
      |   |\                               / \
      T   T * F                          id   id
      |   |   |
      F   F   id
      |   |
      id  id

AST is cleaner — shows operator hierarchy directly.
```

---

## ⚖️ Parse Tree vs AST

| Feature | Parse Tree | AST |
|---------|------------|-----|
| Contains | All grammar symbols | Only semantic content |
| Size | Larger | Smaller |
| Grammar rules | Visible | Hidden |
| Use | Parsing verification | Code generation, analysis |
| Intermediate nodes | Non-terminals | Operators/constructs |

---

## ✏️ Worked Example — Full Parse Tree

```
Grammar:
  S → if E then S | if E then S else S | id := E
  E → id | num | E + E

Input: "if id then id := id + num"

Parse tree:
              S
              |
    ┌─────────┼──────────┐
    if        E         then  S
              |               |
              id         ┌────┼────┐
                         id  :=    E
                                  /|\
                                 E + E
                                 |   |
                                 id  num
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Parse tree leaves must spell out the input string left to right.
> 🚫 **Mistake 2:** AST is NOT the same as parse tree — AST is derived from parse tree by pruning.
> 🚫 **Mistake 3:** An ambiguous grammar produces multiple parse trees for the same string.

---

## ⚡ One-Minute Recap

- Parse tree: full derivation tree, root=S, leaves=terminals
- AST: simplified tree, only semantic structure
- Ambiguous grammar → multiple parse trees for same string
- Parse tree used in parsing | AST used in semantic analysis and code gen

---

## 📝 Probable Exam Questions

> **5-mark:** Draw the parse tree for "a + b * c" using the given grammar. Also draw the AST.
> **Short note:** What is the difference between a parse tree and an abstract syntax tree?
> **Diagram:** Show two different parse trees for "id + id * id" to prove the grammar is ambiguous.

---

---

# 6. FIRST and FOLLOW Sets

## 💡 Intuition First

> **FIRST(A)** answers: "What terminal can appear as the FIRST symbol when A is expanded?"
> **FOLLOW(A)** answers: "What terminal can appear AFTER A in any sentential form?"

These sets are used to build **predictive parsers** (LL(1)) — the parser looks at the next input token and decides which production to use.

**Real-world analogy:** FIRST = "What's the first ingredient in this recipe?" FOLLOW = "What dish comes after this one in the meal?"

---

## 📐 FIRST Set Rules

```
FIRST(X) for terminal X:
  FIRST(X) = {X}

FIRST(X) for non-terminal X:
  For each production X → Y₁Y₂...Yₖ:
    Add FIRST(Y₁) - {ε} to FIRST(X)
    If ε ∈ FIRST(Y₁): add FIRST(Y₂) - {ε}
    If ε ∈ FIRST(Y₁) and ε ∈ FIRST(Y₂): add FIRST(Y₃) - {ε}
    ...
    If ε ∈ FIRST(Yᵢ) for all i: add ε to FIRST(X)

FIRST(ε) = {ε}
```

---

## 📐 FOLLOW Set Rules

```
FOLLOW(S) = {$}  ($ = end of input, S = start symbol)

For each production A → αBβ:
  Add FIRST(β) - {ε} to FOLLOW(B)
  If ε ∈ FIRST(β): add FOLLOW(A) to FOLLOW(B)

For each production A → αB:
  Add FOLLOW(A) to FOLLOW(B)
```

---

## ✏️ Worked Example

```
Grammar:
  E  → T E'
  E' → + T E' | ε
  T  → F T'
  T' → * F T' | ε
  F  → ( E ) | id

Step 1: Compute FIRST sets:

FIRST(F):
  F → (E): FIRST = {(}
  F → id:  FIRST = {id}
  FIRST(F) = {(, id}

FIRST(T'):
  T' → *FT': FIRST = {*}
  T' → ε:    FIRST = {ε}
  FIRST(T') = {*, ε}

FIRST(T):
  T → FT': FIRST(F) = {(, id}
           ε ∉ FIRST(F), so stop
  FIRST(T) = {(, id}

FIRST(E'):
  E' → +TE': FIRST = {+}
  E' → ε:    FIRST = {ε}
  FIRST(E') = {+, ε}

FIRST(E):
  E → TE': FIRST(T) = {(, id}
           ε ∉ FIRST(T), so stop
  FIRST(E) = {(, id}

Step 2: Compute FOLLOW sets:

FOLLOW(E):
  E is start symbol → FOLLOW(E) = {$}
  F → (E): β = ')' → add FIRST(')') = {')'} to FOLLOW(E)
  FOLLOW(E) = {$, )}

FOLLOW(E'):
  E → TE': E' is at end → add FOLLOW(E) = {$, )} to FOLLOW(E')
  FOLLOW(E') = {$, )}

FOLLOW(T):
  E → TE': β = E' → add FIRST(E')-{ε} = {+} to FOLLOW(T)
           ε ∈ FIRST(E') → add FOLLOW(E) = {$, )} to FOLLOW(T)
  FOLLOW(T) = {+, $, )}

FOLLOW(T'):
  T → FT': T' at end → add FOLLOW(T) = {+, $, )} to FOLLOW(T')
  FOLLOW(T') = {+, $, )}

FOLLOW(F):
  T → FT': β = T' → add FIRST(T')-{ε} = {*} to FOLLOW(F)
           ε ∈ FIRST(T') → add FOLLOW(T) = {+, $, )} to FOLLOW(F)
  FOLLOW(F) = {*, +, $, )}

Summary:
  FIRST(E)  = {(, id}
  FIRST(E') = {+, ε}
  FIRST(T)  = {(, id}
  FIRST(T') = {*, ε}
  FIRST(F)  = {(, id}

  FOLLOW(E)  = {$, )}
  FOLLOW(E') = {$, )}
  FOLLOW(T)  = {+, $, )}
  FOLLOW(T') = {+, $, )}
  FOLLOW(F)  = {*, +, $, )}
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** FIRST sets contain terminals only (and possibly ε). FOLLOW sets contain terminals and $ only — never ε.
> 🚫 **Mistake 2:** FOLLOW of start symbol always includes $ (end marker).
> 🚫 **Mistake 3:** When computing FOLLOW(B) from A → αBβ, if ε ∈ FIRST(β), you MUST add FOLLOW(A).
> 🚫 **Mistake 4:** FIRST of a string αβ: if ε ∈ FIRST(α), include FIRST(β) too.

---

## 🎯 Exam Tips

> 💡 Always compute FIRST before FOLLOW — FOLLOW depends on FIRST.
> 💡 FOLLOW never contains ε — if you're adding ε, add FOLLOW of the enclosing non-terminal instead.
> 💡 These sets are used to build the LL(1) parsing table — know the connection.

---

## ⚡ One-Minute Recap

- FIRST(A): terminals that can start strings derived from A
- FOLLOW(A): terminals that can follow A in any derivation
- FIRST rules: look at right side of productions
- FOLLOW rules: look at where A appears on right side of productions
- FOLLOW(start) always contains $

---

## 📝 Probable Exam Questions

> **5-mark:** Compute FIRST and FOLLOW sets for all non-terminals in the given grammar.
> **Short note:** What are FIRST and FOLLOW sets? Why are they needed?
> **Apply:** Use FIRST/FOLLOW to construct the LL(1) parsing table.

---

---

# 7. Left Recursion & Left Factoring

## 💡 Intuition First

> **Left recursion** is a grammar rule that calls itself on the left — like a function that calls itself before doing anything else. Top-down parsers loop forever on this.
>
> **Left factoring** is needed when two productions start with the same symbol — the parser can't decide which rule to use without looking ahead.

---

## 🔄 Left Recursion

### Direct Left Recursion

```
Problem: A → Aα | β
  Parser tries to expand A → Aα → AAα → AAAα → ... (infinite loop!)

Example:
  E → E + T | T   ← left recursive!

Fix — Eliminate left recursion:
  A → Aα | β
  becomes:
  A  → β A'
  A' → α A' | ε

Applied to E → E + T | T:
  E  → T E'
  E' → + T E' | ε
```

### Indirect Left Recursion

```
Problem:
  A → Bα | ...
  B → Aβ | ...
  (A → Bα → Aβα → ... infinite!)

Fix: Substitute to make direct, then eliminate.
  Step 1: Substitute B's production into A:
    A → Aβα | ...
  Step 2: Eliminate direct left recursion.
```

### General Algorithm

```
For each non-terminal Aᵢ (in order i = 1 to n):
  1. Substitute all Aⱼ (j < i) in Aᵢ's productions
  2. Eliminate direct left recursion in Aᵢ
```

---

## 🔀 Left Factoring

### Problem

```
Grammar:
  A → αβ₁ | αβ₂

Parser sees 'α' but can't decide: use αβ₁ or αβ₂?
Need to look further ahead (not LL(1) compatible).

Example:
  stmt → if expr then stmt else stmt
        | if expr then stmt
  Both start with "if expr then stmt" — ambiguous choice!
```

### Fix — Left Factoring

```
A → αβ₁ | αβ₂
becomes:
A  → α A'
A' → β₁ | β₂

Example:
  stmt → if expr then stmt else stmt
        | if expr then stmt

After left factoring:
  stmt  → if expr then stmt stmt'
  stmt' → else stmt | ε
```

### Another Example

```
Before:
  A → abcD | abcE | xyz

After (factor out "abc"):
  A  → abc A' | xyz
  A' → D | E
```

---

## ✏️ Full Worked Example

```
Grammar:
  S → iEtS | iEtSeS | a
  E → b

Step 1: Left factor S:
  S → iEtS S' | a
  S' → eS | ε

Step 2: Check for left recursion → none.

Final grammar:
  S  → iEtS S' | a
  S' → eS | ε
  E  → b

This is the classic "dangling else" problem!
```

---

## ⚖️ Left Recursion vs Left Factoring

| Issue | Problem | Fix |
|-------|---------|-----|
| **Left Recursion** | A → Aα causes infinite loop in top-down parsing | Replace with right recursion using A' |
| **Left Factoring** | A → αβ₁ \| αβ₂ causes ambiguity in choice | Factor out common prefix α |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** After eliminating left recursion, the new A' production must end with `A' | ε`.
> 🚫 **Mistake 2:** Left factoring doesn't eliminate ambiguity — it just makes the grammar LL(1) parseable.
> 🚫 **Mistake 3:** Not all left-recursive grammars can be made LL(1) — some are inherently ambiguous.

---

## ⚡ One-Minute Recap

- Left recursion: A → Aα | β → fix: A → βA', A' → αA' | ε
- Left factoring: A → αβ₁ | αβ₂ → fix: A → αA', A' → β₁ | β₂
- Both transformations needed for LL(1) parsing
- Indirect left recursion: substitute then eliminate

---

## 📝 Probable Exam Questions

> **5-mark:** Eliminate left recursion from: `E → E + T | E - T | T` and `T → T * F | F`.
> **5-mark:** Apply left factoring to: `A → aAB | aB | b`.
> **Short note:** Why must left recursion be eliminated for top-down parsing?

---

---

# 8. Phases of a Compiler

## 💡 Intuition First

> A compiler is like a **translation pipeline** — your source code (English) goes through multiple stages before becoming machine code (binary). Each stage transforms the representation, checking and optimizing along the way.

**Real-world analogy:** Translating a novel from Bengali to English — first understand the words (lexical), then grammar (syntax), then meaning (semantic), then write the translation (code generation).

---

## 🔄 Compiler Phases — Full Pipeline

```
Source Code
    │
    ▼
┌─────────────────────────────────────────────────────┐
│  Phase 1: LEXICAL ANALYSIS (Scanner)                │
│  Input:  Source code characters                     │
│  Output: Stream of tokens                           │
│  Tool:   DFA / Regular expressions                  │
│  Errors: Illegal characters                         │
└─────────────────────────────────────────────────────┘
    │  Token stream
    ▼
┌─────────────────────────────────────────────────────┐
│  Phase 2: SYNTAX ANALYSIS (Parser)                  │
│  Input:  Token stream                               │
│  Output: Parse tree / AST                           │
│  Tool:   CFG / LL(1), LR parsers                   │
│  Errors: Syntax errors (missing ;, unmatched {})    │
└─────────────────────────────────────────────────────┘
    │  Parse tree / AST
    ▼
┌─────────────────────────────────────────────────────┐
│  Phase 3: SEMANTIC ANALYSIS                         │
│  Input:  AST                                        │
│  Output: Annotated AST                              │
│  Tool:   Symbol table, type checking                │
│  Errors: Type mismatch, undeclared variables        │
└─────────────────────────────────────────────────────┘
    │  Annotated AST
    ▼
┌─────────────────────────────────────────────────────┐
│  Phase 4: INTERMEDIATE CODE GENERATION              │
│  Input:  Annotated AST                              │
│  Output: Three-address code / TAC                   │
│  Purpose: Machine-independent representation        │
└─────────────────────────────────────────────────────┘
    │  Intermediate code
    ▼
┌─────────────────────────────────────────────────────┐
│  Phase 5: CODE OPTIMIZATION                         │
│  Input:  Intermediate code                          │
│  Output: Optimized intermediate code                │
│  Techniques: Dead code elimination, loop unrolling  │
└─────────────────────────────────────────────────────┘
    │  Optimized code
    ▼
┌─────────────────────────────────────────────────────┐
│  Phase 6: CODE GENERATION                           │
│  Input:  Optimized intermediate code                │
│  Output: Target machine code / assembly             │
│  Tasks:  Register allocation, instruction selection │
└─────────────────────────────────────────────────────┘
    │
    ▼
Target Code (Assembly / Machine Code)
```

### Supporting Components (run throughout)

```
┌──────────────────┐    ┌──────────────────────┐
│   Symbol Table   │    │   Error Handler      │
│                  │    │                      │
│ Stores: names,   │    │ Detects, reports,    │
│ types, scope,    │    │ and recovers from    │
│ memory location  │    │ errors at each phase │
└──────────────────┘    └──────────────────────┘
```

---

## 📊 Phase Summary Table

| Phase | Input | Output | Errors Caught |
|-------|-------|--------|---------------|
| Lexical Analysis | Characters | Tokens | Illegal chars, invalid tokens |
| Syntax Analysis | Tokens | Parse tree | Grammar violations |
| Semantic Analysis | Parse tree | Annotated AST | Type errors, scope errors |
| IR Generation | Annotated AST | TAC/IR | — |
| Optimization | IR | Optimized IR | — |
| Code Generation | Optimized IR | Machine code | — |

---

## 🔄 Example: Compiling `a = b + c * 2`

```
Source: a = b + c * 2

Phase 1 — Lexical Analysis:
  Tokens: [id:a] [=] [id:b] [+] [id:c] [*] [num:2]

Phase 2 — Syntax Analysis:
  Parse tree:
       assign
      /      \
    id:a      +
             / \
           id:b  *
                / \
              id:c num:2

Phase 3 — Semantic Analysis:
  Check: a, b, c declared? Types compatible?
  Annotate types: b:int, c:int, 2:int → result:int

Phase 4 — IR Generation (Three-Address Code):
  t1 = c * 2
  t2 = b + t1
  a  = t2

Phase 5 — Optimization:
  (if 2 is constant, fold: t1 = c * 2 stays, or inline)

Phase 6 — Code Generation (x86-like):
  MOV R1, c
  MUL R1, 2
  MOV R2, b
  ADD R2, R1
  MOV a, R2
```

---

## ⚖️ Compiler vs Interpreter

| Feature | Compiler | Interpreter |
|---------|----------|-------------|
| Translation | Entire program at once | Line by line |
| Speed | Faster execution | Slower execution |
| Error detection | Before execution | During execution |
| Output | Machine code | Direct execution |
| Examples | C, C++, Java (bytecode) | Python, JavaScript |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Lexical analysis uses DFA/regex — NOT CFG. CFG is for syntax analysis.
> 🚫 **Mistake 2:** Semantic analysis catches type errors — NOT syntax errors.
> 🚫 **Mistake 3:** Symbol table is used across multiple phases, not just one.
> 🚫 **Mistake 4:** Code optimization is optional — a compiler can skip it.

---

## ⚡ One-Minute Recap

- 6 phases: Lexical → Syntax → Semantic → IR Gen → Optimization → Code Gen
- Lexical: chars → tokens (DFA/regex)
- Syntax: tokens → parse tree (CFG/parser)
- Semantic: type checking, symbol table
- IR: machine-independent intermediate form
- Code gen: machine-specific assembly/binary

---

## 📝 Probable Exam Questions

> **5-mark:** Draw and explain all phases of a compiler with input/output of each phase.
> **Short note:** What is the role of the symbol table in a compiler?
> **Trace:** Show the output of each compiler phase for the expression `x = y + z * 3`.
> **Compare:** Compiler vs Interpreter.

---

---

# 9. Lexical Analysis

## 💡 Intuition First

> Lexical analysis is like **reading a sentence word by word**. The scanner reads characters and groups them into meaningful units called **tokens** — just like recognizing "hello" as a word, not individual letters h-e-l-l-o.

---

## 📐 Key Concepts

```
Token:    A meaningful unit — (token_type, attribute_value)
          Examples: <id, "x">, <num, 42>, <+, >, <if, >

Lexeme:   The actual character sequence matched
          e.g., "position", "=", "initial", "+", "rate", "*", "60"

Pattern:  The rule describing what lexemes match a token
          e.g., letter(letter|digit)* matches identifiers
```

### Token Categories

| Token Type | Examples | Pattern |
|------------|---------|---------|
| **Keywords** | if, while, for, int | Fixed strings |
| **Identifiers** | x, myVar, count | letter(letter\|digit)* |
| **Numbers** | 42, 3.14 | digit+ or digit+.digit+ |
| **Operators** | +, -, *, /, =, == | Fixed symbols |
| **Delimiters** | (, ), {, }, ; | Fixed symbols |
| **Strings** | "hello" | "any chars" |

---

## 🔄 Lexical Analysis Process

```
Source: position = initial + rate * 60

Lexer output (token stream):
  <id, "position">
  <=, >
  <id, "initial">
  <+, >
  <id, "rate">
  <*, >
  <num, 60>

Symbol table after lexical analysis:
  position → entry 1
  initial  → entry 2
  rate     → entry 3
```

---

## 🔄 DFA for Identifiers

```
Identifier pattern: letter (letter | digit)*

DFA:
         letter          letter | digit
  →(q0) ──────────► (q1) ──────────────► (q1)
                    (accept)

State q0: start
State q1: accept (identifier recognized)

Trace "rate":
  q0 →(r)→ q1 →(a)→ q1 →(t)→ q1 →(e)→ q1
  End of token → ACCEPT, lexeme = "rate"
```

---

## 🔄 DFA for Numbers

```
Integer: digit+
Float:   digit+ . digit+

DFA:
         digit           digit
  →(q0) ──────► (q1) ──────────► (q1)  [integer accept]
                  │
                  . (dot)
                  │
                 (q2) ──digit──► (q3)   [float accept]
                                  │
                                 digit
                                  └──────────────┘
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Keywords are recognized as identifiers first, then checked against a keyword table.
> 🚫 **Mistake 2:** Whitespace and comments are consumed (skipped) by the lexer — not passed to parser.
> 🚫 **Mistake 3:** Lexical errors (illegal character like @) are caught here, not in syntax analysis.

---

## ⚡ One-Minute Recap

- Lexer: source chars → token stream
- Token = (type, value) | Lexeme = actual string | Pattern = regex rule
- Implemented using DFA (one DFA per token type, combined)
- Skips whitespace and comments
- Builds/updates symbol table

---

## 📝 Probable Exam Questions

> **Short note:** What is a token? Give examples of different token types.
> **Design:** Draw a DFA to recognize floating-point numbers.
> **Trace:** Tokenize the expression `if (x >= 10) y = x + 1;`

---

# 10. Parsing

## 💡 Intuition First

> Parsing is like **checking grammar in a sentence**. The parser takes the token stream and verifies it follows the language's grammar rules, building a parse tree in the process.

---

## 📐 Types of Parsers

```
Parsing
├── Top-Down (builds tree from root to leaves)
│   ├── Recursive Descent (manual, one function per non-terminal)
│   └── LL(1) (table-driven, Left-to-right, Leftmost derivation, 1 lookahead)
│
└── Bottom-Up (builds tree from leaves to root)
    ├── LR(0)
    ├── SLR(1) (Simple LR)
    ├── LALR(1) (Lookahead LR) ← most common (used in yacc/bison)
    └── LR(1) (Canonical LR)
```

---

## 🔼 LL(1) Parsing

> **L**eft-to-right scan, **L**eftmost derivation, **1** token lookahead.

### LL(1) Parsing Table Construction

```
For each production A → α:
  For each terminal a in FIRST(α):
    Add A → α to M[A, a]
  If ε ∈ FIRST(α):
    For each terminal b in FOLLOW(A):
      Add A → α to M[A, b]
    If $ ∈ FOLLOW(A):
      Add A → α to M[A, $]
```

### LL(1) Table Example

```
Grammar (after left recursion elimination):
  E  → T E'
  E' → + T E' | ε
  T  → F T'
  T' → * F T' | ε
  F  → ( E ) | id

Using FIRST/FOLLOW computed earlier:

LL(1) Parsing Table:
        id      +       *       (       )       $
E    E→TE'              E→TE'
E'          E'→+TE'             E'→ε    E'→ε
T    T→FT'              T→FT'
T'          T'→ε    T'→*FT'             T'→ε    T'→ε
F    F→id               F→(E)
```

### LL(1) Parse Trace

```
Input: id + id * id $

Stack (top→bottom)  │ Input          │ Action
────────────────────┼────────────────┼──────────────────
$ E                 │ id+id*id$      │ M[E,id] = E→TE'
$ E' T              │ id+id*id$      │ M[T,id] = T→FT'
$ E' T' F           │ id+id*id$      │ M[F,id] = F→id
$ E' T' id          │ id+id*id$      │ Match id, pop
$ E' T'             │ +id*id$        │ M[T',+] = T'→ε
$ E'                │ +id*id$        │ M[E',+] = E'→+TE'
$ E' T +            │ +id*id$        │ Match +, pop
$ E' T              │ id*id$         │ M[T,id] = T→FT'
$ E' T' F           │ id*id$         │ M[F,id] = F→id
$ E' T' id          │ id*id$         │ Match id, pop
$ E' T'             │ *id$           │ M[T',*] = T'→*FT'
$ E' T' F *         │ *id$           │ Match *, pop
$ E' T' F           │ id$            │ M[F,id] = F→id
$ E' T' id          │ id$            │ Match id, pop
$ E' T'             │ $              │ M[T',$] = T'→ε
$ E'                │ $              │ M[E',$] = E'→ε
$                   │ $              │ ACCEPT ✅
```

---

## 🔽 LR Parsing (Bottom-Up)

> Reads input left to right, builds parse tree bottom-up. Uses a **stack** and **action/goto tables**.

```
Two actions:
  SHIFT:  Push next input token onto stack
  REDUCE: Pop symbols matching right side of production,
          push left side (non-terminal)

Accept when: Stack = [S] and input = [$]

LR > LL in power:
  LR can handle more grammars (left-recursive, etc.)
  LL(1) ⊂ LR(1) in terms of grammars handled
```

---

## ⚖️ LL vs LR Parsing

| Feature | LL(1) | LR(1) |
|---------|-------|-------|
| Direction | Top-down | Bottom-up |
| Derivation | Leftmost | Rightmost (reversed) |
| Stack content | Non-terminals | States + symbols |
| Grammar power | Less powerful | More powerful |
| Left recursion | ❌ Cannot handle | ✅ Can handle |
| Implementation | Simpler | Complex |
| Tools | Recursive descent | yacc, bison |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** LL(1) cannot handle left-recursive grammars — must eliminate first.
> 🚫 **Mistake 2:** A grammar is LL(1) only if the parsing table has NO conflicts (no cell with 2+ entries).
> 🚫 **Mistake 3:** LR parsers are more powerful — they can handle a superset of LL(1) grammars.

---

## ⚡ One-Minute Recap

- LL(1): top-down, leftmost, 1 lookahead, uses FIRST/FOLLOW for table
- LR: bottom-up, shift-reduce, more powerful
- LL(1) table: M[A, a] = production to use
- Conflict in LL(1) table → grammar is not LL(1)

---

## 📝 Probable Exam Questions

> **5-mark:** Construct the LL(1) parsing table for the given grammar. Trace parsing of a given string.
> **Short note:** What is a shift-reduce conflict in LR parsing?
> **Compare:** LL(1) vs LR(1) parsing.

---

---

# 11. Code Generation

## 💡 Intuition First

> Code generation is the final translation step — converting the optimized intermediate representation into actual machine instructions. Like translating a mathematical formula into assembly language step by step.

---

## 📐 Three-Address Code (TAC / IR)

> The most common intermediate representation. Each instruction has at most 3 operands.

```
TAC instruction forms:
  x = y op z      (binary operation)
  x = op y        (unary operation)
  x = y           (copy)
  goto L          (unconditional jump)
  if x goto L     (conditional jump)
  param x         (function parameter)
  call f, n       (function call)
  return x        (return value)

Example: a = b + c * d - e

TAC:
  t1 = c * d
  t2 = b + t1
  t3 = t2 - e
  a  = t3
```

---

## 🔄 Code Generation Example

```
Source: x = a + b * c

TAC:
  t1 = b * c
  t2 = a + t1
  x  = t2

Assembly (x86-like):
  MOV R1, b      ; R1 = b
  MUL R1, c      ; R1 = b * c  (t1)
  MOV R2, a      ; R2 = a
  ADD R2, R1     ; R2 = a + t1 (t2)
  MOV x, R2      ; x = t2
```

---

## 🔧 Code Optimization Techniques

| Technique | Description | Example |
|-----------|-------------|---------|
| **Constant folding** | Evaluate constant expressions at compile time | `2 * 3` → `6` |
| **Dead code elimination** | Remove unreachable code | Code after `return` |
| **Common subexpression** | Reuse already-computed values | `a+b` computed twice → compute once |
| **Loop invariant** | Move constant computations out of loops | `x = a*b` inside loop → move outside |
| **Strength reduction** | Replace expensive ops with cheaper ones | `x*2` → `x+x` or `x<<1` |
| **Register allocation** | Keep frequently used values in registers | Minimize memory accesses |

---

## 📊 Compiler Tools

| Tool | Purpose | Example |
|------|---------|---------|
| **lex / flex** | Lexical analyzer generator | Generates scanner from regex |
| **yacc / bison** | Parser generator | Generates parser from CFG |
| **LLVM** | Compiler infrastructure | Used by Clang, Rust |
| **GCC** | GNU Compiler Collection | C, C++, Fortran |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** TAC is machine-independent — it's not assembly code.
> 🚫 **Mistake 2:** Optimization is optional — correctness must be preserved.
> 🚫 **Mistake 3:** Register allocation is NP-complete in general — compilers use heuristics.

---

## ⚡ One-Minute Recap

- TAC: intermediate code, at most 3 operands per instruction
- Code gen: TAC → machine-specific assembly
- Optimization: constant folding, dead code elimination, loop invariant
- Tools: lex (lexer), yacc (parser), LLVM (IR + backend)

---

## 📝 Probable Exam Questions

> **5-mark:** Generate three-address code for the expression `a = b * c + d / e - f`.
> **Short note:** What is constant folding? Give an example.
> **Trace:** Show the TAC and assembly code for `if (x > 0) y = x + 1; else y = -x;`

---

---

# 🏁 Master Quick Revision Sheet — Compiler Design & Automata

## ⚡ Automata Hierarchy

```
Regular Languages (DFA/NFA/Regex)
    ⊂
Context-Free Languages (CFG/PDA)
    ⊂
Context-Sensitive Languages (CSG/LBA)
    ⊂
Recursively Enumerable (Turing Machine)

Examples:
  Regular:        a*b, identifiers, keywords
  Context-Free:   aⁿbⁿ, balanced parentheses, arithmetic expressions
  NOT Regular:    aⁿbⁿ (needs counting → stack)
  NOT CF:         aⁿbⁿcⁿ (needs 2 stacks → Turing machine)
```

## 🔑 Key Facts to Remember

| Fact | Detail |
|------|--------|
| DFA vs NFA | Same power (regular languages), NFA → DFA via subset construction |
| NFA states after conversion | Up to 2ⁿ DFA states from n NFA states |
| ε-closure | Set of states reachable via ε-transitions only |
| Left recursion fix | A → Aα\|β becomes A → βA', A' → αA'\|ε |
| Left factoring fix | A → αβ₁\|αβ₂ becomes A → αA', A' → β₁\|β₂ |
| FIRST never contains | — (can contain ε) |
| FOLLOW never contains | ε (only terminals and $) |
| LL(1) conflict | Two entries in same cell → not LL(1) |
| LR > LL | LR handles left-recursive grammars |
| Compiler phases | 6: Lex → Syn → Sem → IR → Opt → CodeGen |
| Lexical tool | DFA / regex (lex/flex) |
| Syntax tool | CFG / LL or LR parser (yacc/bison) |

## 🧠 Memory Tricks

- **Compiler phases:** "**L**azy **S**tudents **S**ometimes **I**gnore **O**ld **C**oncepts" → Lexical, Syntax, Semantic, IR, Optimization, Code gen
- **DFA vs NFA:** "**D**efinite **D**irection" vs "**N**umerous **N**ondeterministic paths"
- **FIRST/FOLLOW:** "FIRST = what comes **first** | FOLLOW = what comes **after**"
- **LL vs LR:** "**LL** = **L**ook ahead **L**eft | **LR** = **L**ook at **R**ight side"
- **Chomsky types:** "**T**uring **C**an **C**reate **R**egular" → Type 0,1,2,3 (reversed)

## 🎯 Top 10 Most Probable Exam Questions

1. Design DFA for a given language — draw state diagram + transition table
2. Convert NFA to DFA using subset construction
3. Eliminate left recursion from a given grammar
4. Apply left factoring to a given grammar
5. Compute FIRST and FOLLOW sets for all non-terminals
6. Construct LL(1) parsing table and trace a string
7. Draw parse tree and AST for a given expression
8. Show all phases of compiler with example
9. Generate three-address code for an expression
10. Prove a grammar is ambiguous (show two parse trees)

## 📊 Automata Quick Reference

```
┌──────────────┬──────────────┬──────────────┬──────────────┐
│ Automaton    │ Memory       │ Language     │ Example      │
├──────────────┼──────────────┼──────────────┼──────────────┤
│ DFA/NFA      │ States only  │ Regular      │ a*b          │
│ PDA          │ Stack        │ Context-Free │ aⁿbⁿ         │
│ LBA          │ Bounded tape │ Context-Sens │ aⁿbⁿcⁿ       │
│ Turing Mach  │ Infinite tape│ RE           │ Halting prob │
└──────────────┴──────────────┴──────────────┴──────────────┘
```

---

> 📌 **End of Subject 04: Compiler Design & Automata**
>
> Next: **Subject 05 — Digital Logic Design** →

---

*Handbook generated for MSc Admission Preparation | JUST-Style Exam Focus*
*Version 1.0 | Compiler Design & Automata*
