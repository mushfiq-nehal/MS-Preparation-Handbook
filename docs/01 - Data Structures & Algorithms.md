# 📘 MSc Admission Prep — Subject 01: Data Structures & Algorithms
### 🎯 JUST-Style Exam Handbook | Fast Revision Edition

> **Who this is for:** BSc graduates who studied DSA but need a fast, deep, visual refresh before the MSc admission exam.
> **How to use:** Read the intuition first. Then the formal definition. Then trace the examples. Finish with exam tips.

---

## 📋 Table of Contents

| # | Topic | Tier |
|---|-------|------|
| 1 | [Linked List](#1-linked-list) | 🔴 Must Master |
| 2 | [Stack & Queue](#2-stack--queue) | 🔴 Must Master |
| 3 | [Trees & BST](#3-trees--bst) | 🔴 Must Master |
| 4 | [Hashing](#4-hashing) | 🔴 Must Master |
| 5 | [Binary Search](#5-binary-search) | 🔴 Must Master |
| 6 | [Sorting Algorithms](#6-sorting-algorithms) | 🔴 Must Master |
| 7 | [Dynamic Programming](#7-dynamic-programming) | 🔴 Must Master |
| 8 | [Greedy Algorithms](#8-greedy-algorithms) | 🔴 Must Master |
| 9 | [Graph Algorithms](#9-graph-algorithms) | 🔴 Must Master |
| 10 | [Complexity Analysis](#10-complexity-analysis) | 🔴 Must Master |

---

---

# 1. Linked List

## 💡 Intuition First

> Imagine a **treasure hunt** — each clue tells you where the next clue is. You can't jump to clue #5 directly; you must follow the chain from clue #1.

That's a linked list. Each **node** holds data + a pointer to the next node. Unlike arrays, nodes are **not stored contiguously** in memory.

**Real-world analogy:** A train — each coach is connected to the next. You can add/remove coaches anywhere without rebuilding the whole train.

**Why it matters:** Linked lists are the foundation of stacks, queues, hash chaining, and adjacency lists. Exam questions love insertion/deletion and reversal.

---

## 📐 Formal Definition

A **Linked List** is a linear data structure where each element (node) contains:
- `data` — the value stored
- `next` — a pointer/reference to the next node

The list starts at a **head** pointer. The last node points to `NULL`.

```
HEAD
 │
 ▼
[10 | •]──►[20 | •]──►[30 | •]──►[40 | NULL]
```

### Types

| Type | Description |
|------|-------------|
| **Singly Linked** | Each node points to next only |
| **Doubly Linked** | Each node points to next AND previous |
| **Circular** | Last node points back to head |

---

## 🔧 Core Operations

### ➕ Insertion

**Three cases:**
1. At the **beginning** (before head)
2. At the **end** (after last node)
3. At a **specific position**

#### Insert at Beginning — Step-by-Step

```
Before: HEAD → [10]→[20]→[30]→NULL
Insert 5 at beginning

Step 1: Create new node [5]
Step 2: new_node.next = HEAD        → [5]→[10]→[20]→[30]→NULL
Step 3: HEAD = new_node

After:  HEAD → [5]→[10]→[20]→[30]→NULL
```

**Pseudocode:**
```
function insertAtBeginning(head, value):
    new_node = Node(value)
    new_node.next = head
    head = new_node
    return head
```

#### Insert at End

```
Before: HEAD → [10]→[20]→[30]→NULL
Insert 40 at end

Step 1: Create new node [40], new_node.next = NULL
Step 2: Traverse to last node (node where next == NULL)
Step 3: last_node.next = new_node

After:  HEAD → [10]→[20]→[30]→[40]→NULL
```

#### Sorted Insertion

```
List: [10]→[30]→[50]→NULL   Insert: 25

Step 1: Find position where prev.data < 25 < curr.data
        prev = [10], curr = [30]
Step 2: new_node.next = curr   → [25]→[30]
Step 3: prev.next = new_node   → [10]→[25]→[30]

Result: [10]→[25]→[30]→[50]→NULL
```

---

### ➖ Deletion

**Three cases:** Delete from beginning, end, or by value.

```
List: HEAD → [10]→[20]→[30]→[40]→NULL
Delete node with value 30

Step 1: Traverse to find node BEFORE 30 → that's [20]
Step 2: prev.next = curr.next   → [20].next = [40]
Step 3: Free/delete curr ([30])

Result: HEAD → [10]→[20]→[40]→NULL
```

---

### 🔄 Reversal

> Think of reversing a chain of arrows. Each arrow that pointed forward must now point backward.

```
Before: [1]→[2]→[3]→[4]→NULL

Step-by-step pointer manipulation:
prev=NULL, curr=HEAD=[1]

Iteration 1: next=[2], [1].next=NULL, prev=[1], curr=[2]
Iteration 2: next=[3], [2].next=[1], prev=[2], curr=[3]
Iteration 3: next=[4], [3].next=[2], prev=[3], curr=[4]
Iteration 4: next=NULL,[4].next=[3], prev=[4], curr=NULL

HEAD = prev = [4]
After: [4]→[3]→[2]→[1]→NULL
```

**Pseudocode:**
```
function reverse(head):
    prev = NULL
    curr = head
    while curr != NULL:
        next = curr.next
        curr.next = prev
        prev = curr
        curr = next
    return prev   ← new head
```

---

## ⚖️ Array vs Linked List

| Feature | Array | Linked List |
|---------|-------|-------------|
| Memory | Contiguous | Scattered |
| Access | O(1) random | O(n) sequential |
| Insertion (middle) | O(n) shift | O(1) after finding position |
| Deletion (middle) | O(n) shift | O(1) after finding position |
| Size | Fixed (static) | Dynamic |
| Cache performance | ✅ Better | ❌ Worse |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Forgetting to update `HEAD` when inserting/deleting at the beginning.
> 🚫 **Mistake 2:** Not handling the `NULL` check before accessing `node.next`.
> 🚫 **Mistake 3:** In reversal, losing the `next` pointer before redirecting it.
> 🚫 **Mistake 4:** Confusing "delete node with value X" vs "delete node at position X".

---

## 🎯 Exam Tips

> 💡 **Tip 1:** Exam questions often ask you to **trace** insertion/deletion step by step. Draw boxes and arrows.
> 💡 **Tip 2:** Reversal is a **very high-frequency** question. Memorize the 3-pointer technique (prev, curr, next).
> 💡 **Tip 3:** Sorted insertion requires finding the **correct position** — always check boundary conditions (insert at head, insert at tail).
> 💡 **Tip 4:** Time complexity: All operations are **O(n)** except insert-at-head which is **O(1)**.

---

## ⚡ One-Minute Recap

- Node = data + pointer
- Insert at head: O(1) | Insert at end: O(n) | Search: O(n)
- Reversal uses 3 pointers: `prev`, `curr`, `next`
- Sorted insertion: traverse until `prev.data < val < curr.data`
- Advantage over array: dynamic size, efficient mid-insertion

---

## 🎓 Viva-Style Quick Questions

1. What is the time complexity of searching in a linked list?
2. How do you detect a cycle in a linked list? *(Floyd's algorithm)*
3. What happens if you lose the `head` pointer?
4. How is a doubly linked list different from singly?
5. Can you access the 5th element in O(1)? Why not?

---

## 📝 Probable Exam Questions

> **5-mark:** Write an algorithm to reverse a singly linked list. Trace it with example `[1→2→3→4→5]`.
> **5-mark:** Write a function to insert a node in a sorted linked list.
> **Short note:** Compare array and linked list with respect to time complexity of operations.
> **Diagram:** Draw the memory representation of a doubly linked list with 3 nodes.

---

---

# 2. Stack & Queue

## 💡 Intuition First

**Stack** → Think of a **stack of plates**. You always add/remove from the top. Last plate placed = first plate taken. **LIFO** (Last In, First Out).

**Queue** → Think of a **line at a ticket counter**. First person in line = first person served. **FIFO** (First In, First Out).

**Real-world analogies:**
- Stack: Browser back button, undo/redo, function call stack
- Queue: Print queue, CPU scheduling, BFS traversal

---

## 📐 Stack — Core Concepts

```
PUSH 10, 20, 30:

     [30]  ← TOP
     [20]
     [10]
    ──────
```

### Operations

| Operation | Description | Time |
|-----------|-------------|------|
| `push(x)` | Add x to top | O(1) |
| `pop()` | Remove from top | O(1) |
| `peek()/top()` | View top without removing | O(1) |
| `isEmpty()` | Check if empty | O(1) |

### Array Implementation

```
stack = []
top = -1
MAX = 5

push(x):
    if top == MAX-1: OVERFLOW
    top = top + 1
    stack[top] = x

pop():
    if top == -1: UNDERFLOW
    x = stack[top]
    top = top - 1
    return x
```

### Stack Applications

| Application | How Stack Helps |
|-------------|-----------------|
| **Expression evaluation** | Infix → Postfix conversion |
| **Balanced parentheses** | Push `(`, pop on `)` |
| **Function call stack** | Return addresses stored |
| **DFS traversal** | Explicit stack or recursion |
| **Undo operation** | Each action pushed, undo pops |

#### ✏️ Worked Example: Balanced Parentheses

```
Input: { [ ( ) ] }

Process:
  { → push  → stack: [{ ]
  [ → push  → stack: [{, []
  ( → push  → stack: [{, [, (]
  ) → pop   → matches (, stack: [{, []
  ] → pop   → matches [, stack: [{]
  } → pop   → matches {, stack: []

Stack empty at end → BALANCED ✅
```

---

## 📐 Queue — Core Concepts

```
ENQUEUE 10, 20, 30:

FRONT → [10][20][30] ← REAR
```

### Operations

| Operation | Description | Time |
|-----------|-------------|------|
| `enqueue(x)` | Add to rear | O(1) |
| `dequeue()` | Remove from front | O(1) |
| `front()` | View front element | O(1) |
| `isEmpty()` | Check if empty | O(1) |

### Types of Queue

| Type | Description |
|------|-------------|
| **Simple Queue** | Basic FIFO |
| **Circular Queue** | Rear wraps around to front |
| **Priority Queue** | Highest priority served first |
| **Deque** | Insert/delete from both ends |

### Circular Queue — Why?

> In a simple array queue, after many enqueue/dequeue operations, the front moves right and space at the beginning is wasted. Circular queue reuses that space.

```
Circular Queue (size=5):
After some operations:
  front=2, rear=4
  [_, _, 30, 40, 50]

Enqueue 60:
  rear = (rear+1) % 5 = 0
  [60, _, 30, 40, 50]
```

---

## ⚖️ Stack vs Queue

| Feature | Stack | Queue |
|---------|-------|-------|
| Order | LIFO | FIFO |
| Insert | Top | Rear |
| Delete | Top | Front |
| Use case | DFS, undo, recursion | BFS, scheduling, buffering |
| Analogy | Plate stack | Ticket line |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Confusing LIFO and FIFO — Stack is LIFO, Queue is FIFO.
> 🚫 **Mistake 2:** Stack overflow ≠ underflow. Overflow = push on full stack. Underflow = pop on empty stack.
> 🚫 **Mistake 3:** In circular queue, full condition: `(rear+1) % size == front`, NOT `rear == size-1`.

---

## 🎯 Exam Tips

> 💡 Stack is used in **infix to postfix** conversion — very common exam question.
> 💡 Queue is used in **BFS** — always mention this connection.
> 💡 Know the **circular queue** full/empty conditions by heart.
> 💡 Be ready to **trace** push/pop operations step by step.

---

## ⚡ One-Minute Recap

- Stack: LIFO | push/pop from top | used in DFS, recursion, expression eval
- Queue: FIFO | enqueue at rear, dequeue from front | used in BFS, scheduling
- Circular queue solves wasted space problem
- Priority queue: not FIFO — highest priority goes first

---

## 📝 Probable Exam Questions

> **5-mark:** Convert infix expression `A + B * C - D` to postfix using a stack. Show all steps.
> **5-mark:** Implement a circular queue with enqueue, dequeue, and isFull operations.
> **Short note:** Differentiate between stack and queue with examples.
> **Trace:** Given a sequence of push/pop operations, show the stack state after each step.

---

---

# 3. Trees & BST

## 💡 Intuition First

> A **tree** is like a family tree or a company org chart — one boss (root) at the top, with branches going down. No cycles, no loops.

A **Binary Search Tree (BST)** adds a rule: **left child < parent < right child**. This makes searching super fast — like a phone book where you always know which half to look in.

**Real-world analogy:** File system folders. `/home` is root, `/home/user` is a child, `/home/user/docs` is a grandchild.

---

## 📐 Tree Terminology

```
           [50]          ← Root
          /    \
       [30]    [70]      ← Level 1
       /  \    /  \
     [20][40][60][80]    ← Level 2 (Leaf nodes)
```

| Term | Meaning |
|------|---------|
| **Root** | Topmost node (no parent) |
| **Leaf** | Node with no children |
| **Height** | Longest path from root to leaf |
| **Depth** | Distance from root to a node |
| **Degree** | Number of children of a node |
| **Subtree** | A node and all its descendants |

---

## 🌲 Binary Tree Traversals

> **Memory trick:** Think of when you **visit the root** relative to children.
> - **Pre**order = Root **Pre**cedes children (Root, Left, Right)
> - **In**order = Root **In** between children (Left, Root, Right)
> - **Post**order = Root **Post**pones to after children (Left, Right, Root)

```
Tree:
        [1]
       /   \
     [2]   [3]
    /   \
  [4]   [5]
```

| Traversal | Order | Result |
|-----------|-------|--------|
| **Preorder** | Root → Left → Right | 1, 2, 4, 5, 3 |
| **Inorder** | Left → Root → Right | 4, 2, 5, 1, 3 |
| **Postorder** | Left → Right → Root | 4, 5, 2, 3, 1 |
| **Level-order** | Level by level (BFS) | 1, 2, 3, 4, 5 |

> 🔑 **Key fact:** Inorder traversal of a BST gives elements in **sorted order**.

### Pseudocode — Inorder

```
function inorder(node):
    if node == NULL: return
    inorder(node.left)
    print(node.data)
    inorder(node.right)
```

---

## 🔍 BST — Insert, Search, Delete

### BST Property

```
For every node N:
  All nodes in LEFT subtree < N.data
  All nodes in RIGHT subtree > N.data
```

### BST Insertion — Trace

```
Insert: 50, 30, 70, 20, 40, 60, 80

Start: empty

Insert 50 → root = [50]
Insert 30 → 30 < 50 → go left → [50].left = [30]
Insert 70 → 70 > 50 → go right → [50].right = [70]
Insert 20 → 20 < 50 → left → 20 < 30 → left → [30].left = [20]
Insert 40 → 40 < 50 → left → 40 > 30 → right → [30].right = [40]
Insert 60 → 60 > 50 → right → 60 < 70 → left → [70].left = [60]
Insert 80 → 80 > 50 → right → 80 > 70 → right → [70].right = [80]

Final BST:
           [50]
          /    \
       [30]    [70]
       /  \    /  \
     [20][40][60][80]
```

### BST Search — Trace

```
Search 40 in above BST:

Step 1: 40 < 50 → go left to [30]
Step 2: 40 > 30 → go right to [40]
Step 3: 40 == 40 → FOUND ✅

Time: O(h) where h = height of tree
Best case (balanced): O(log n)
Worst case (skewed): O(n)
```

### BST Deletion — 3 Cases

```
Case 1: Delete LEAF node (no children)
  Delete 20: Simply remove it. [30].left = NULL

Case 2: Delete node with ONE child
  Delete 30 (has children 20 and 40... wait, that's 2)
  Delete 60 (has no children — leaf case)
  Example: if [30] had only [20]:
    [50].left = [20]  (bypass [30])

Case 3: Delete node with TWO children
  Delete 50 (root, has both children):
  Step 1: Find INORDER SUCCESSOR (smallest in right subtree) = 60
  Step 2: Replace 50's data with 60
  Step 3: Delete 60 from right subtree

  Result:
           [60]
          /    \
       [30]    [70]
       /  \       \
     [20][40]    [80]
```

### Delete Leaf/Terminal Nodes

```
"Delete all leaf nodes" — common exam question

Tree:           [1]
               /   \
             [2]   [3]
            /   \
          [4]   [5]

Leaf nodes: 4, 5, 3

After deletion:
             [1]
            /
          [2]

Algorithm: Postorder traversal — if node is leaf, delete it
```

---

## ⚖️ BST vs Binary Tree

| Feature | Binary Tree | BST |
|---------|-------------|-----|
| Structure | At most 2 children | At most 2 children |
| Ordering | No rule | Left < Root < Right |
| Search | O(n) | O(log n) avg |
| Inorder | Random | Sorted sequence |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Confusing inorder (sorted) with preorder (root first).
> 🚫 **Mistake 2:** In BST deletion with 2 children, using predecessor instead of successor (both are valid, but be consistent).
> 🚫 **Mistake 3:** Forgetting that a skewed BST degrades to O(n) — it becomes a linked list.
> 🚫 **Mistake 4:** Level-order traversal uses a **queue**, not recursion.

---

## 🎯 Exam Tips

> 💡 **Inorder of BST = sorted output** — this is a guaranteed exam fact.
> 💡 BST deletion with 2 children: always use **inorder successor** (smallest in right subtree).
> 💡 Be ready to **draw the BST** after a sequence of insertions.
> 💡 Traversal questions: write the output sequence AND the pseudocode.

---

## ⚡ One-Minute Recap

- Tree: hierarchical, no cycles, one root
- BST: left < root < right | search O(log n) avg
- Traversals: Pre(RLR), In(LRR), Post(LRR) — R=Root, L=Left, Ri=Right
- Inorder of BST → sorted order
- Delete with 2 children → replace with inorder successor

---

## 📝 Probable Exam Questions

> **5-mark:** Insert the following into a BST: `15, 10, 20, 8, 12, 17, 25`. Draw the tree and write inorder traversal.
> **5-mark:** Write the algorithm for BST deletion. Handle all three cases.
> **Short note:** What is the difference between a binary tree and a BST?
> **Trace:** Delete node 15 from the BST you built above. Show all steps.

---

---

# 4. Hashing

## 💡 Intuition First

> Imagine a library with 1000 books. Instead of searching shelf by shelf, you use a **catalog system** — the book's ID maps directly to its shelf number. That's hashing.

A **hash function** converts a key into an index. Ideally, every key maps to a unique index. But sometimes two keys map to the same index — that's a **collision**.

**Real-world analogy:** Phone contacts sorted by first letter. "Alice" → A section. Fast lookup, but two "A" names need a collision strategy.

---

## 📐 Hash Function

```
hash(key) = key % table_size

Example: table_size = 10
  hash(23) = 23 % 10 = 3  → store at index 3
  hash(45) = 45 % 10 = 5  → store at index 5
  hash(33) = 33 % 10 = 3  → COLLISION with 23!
```

---

## 💥 Collision Resolution

### Method 1: Chaining (Open Hashing)

> Each slot holds a **linked list** of all keys that hash to that index.

```
Table size = 7, Insert: 10, 20, 15, 7, 17

hash(10) = 10%7 = 3
hash(20) = 20%7 = 6
hash(15) = 15%7 = 1
hash(7)  = 7%7  = 0
hash(17) = 17%7 = 3  ← collision with 10!

Hash Table:
Index 0: [7] → NULL
Index 1: [15] → NULL
Index 2: NULL
Index 3: [10] → [17] → NULL   ← chain!
Index 4: NULL
Index 5: NULL
Index 6: [20] → NULL
```

### Method 2: Open Addressing (Closed Hashing)

> All elements stored **inside** the table. On collision, probe for next empty slot.

#### Linear Probing

```
hash(key, i) = (hash(key) + i) % table_size

Insert 10, 20, 15, 7, 17 into table of size 7:

hash(10) = 3 → slot 3 empty → store 10 at 3
hash(20) = 6 → slot 6 empty → store 20 at 6
hash(15) = 1 → slot 1 empty → store 15 at 1
hash(7)  = 0 → slot 0 empty → store 7 at 0
hash(17) = 3 → slot 3 FULL → probe slot 4 → empty → store 17 at 4

Table: [7, 15, _, 10, 17, _, 20]
Index:  0   1  2   3   4  5   6
```

#### Quadratic Probing

```
hash(key, i) = (hash(key) + i²) % table_size

On collision: try i=1 (offset 1), i=2 (offset 4), i=3 (offset 9)...
Reduces clustering compared to linear probing.
```

#### Double Hashing

```
hash(key, i) = (h1(key) + i * h2(key)) % table_size

h2(key) must never be 0 and should be relatively prime to table_size.
Best collision avoidance among open addressing methods.
```

---

## ⚖️ Chaining vs Open Addressing

| Feature | Chaining | Open Addressing |
|---------|----------|-----------------|
| Storage | Extra linked list nodes | Within table only |
| Load factor | Can exceed 1 | Must stay < 1 |
| Deletion | Easy (remove from list) | Complex (mark as deleted) |
| Cache performance | Poor (pointer chasing) | Better (contiguous) |
| Clustering | No | Yes (linear probing worst) |
| Best for | High load factor | Low load factor |

---

## 📊 Load Factor

```
Load Factor (α) = n / m
  n = number of elements
  m = table size

α < 0.7 → good performance
α > 0.7 → consider resizing (rehashing)
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Thinking chaining requires load factor < 1. It doesn't — chains can grow.
> 🚫 **Mistake 2:** In linear probing, forgetting to wrap around (use modulo).
> 🚫 **Mistake 3:** Confusing open hashing (chaining) with open addressing — the names are counterintuitive!
> 🚫 **Mistake 4:** Primary clustering is a problem with **linear probing**, not chaining.

---

## 🎯 Exam Tips

> 💡 **Chaining = linked lists at each slot** | **Open addressing = probe within table**
> 💡 Linear probing causes **primary clustering** — keys bunch together.
> 💡 Average search time with chaining: O(1 + α) where α = load factor.
> 💡 Be ready to **trace** insertions into a hash table showing collision resolution.

---

## ⚡ One-Minute Recap

- Hash function maps key → index
- Collision: two keys → same index
- Chaining: linked list at each slot
- Open addressing: probe for next slot (linear, quadratic, double hashing)
- Load factor α = n/m; keep below 0.7 for efficiency

---

## 📝 Probable Exam Questions

> **5-mark:** Insert keys `{27, 43, 3, 16, 69, 58, 72}` into a hash table of size 10 using linear probing with `h(k) = k % 10`. Show the final table.
> **5-mark:** Explain chaining as a collision resolution technique with a diagram.
> **Short note:** Compare chaining and open addressing.
> **Conceptual:** What is primary clustering? How does quadratic probing reduce it?

---

---

# 5. Binary Search

## 💡 Intuition First

> You're looking for a word in a dictionary. You don't start from page 1 — you open the middle, check if your word comes before or after, then repeat on the relevant half. That's binary search.

**Requirement:** The array must be **sorted**.
**Key idea:** Each comparison eliminates **half** the remaining elements.

---

## 📐 Algorithm

```
function binarySearch(arr, target):
    low = 0
    high = len(arr) - 1

    while low <= high:
        mid = (low + high) / 2

        if arr[mid] == target:
            return mid          ← FOUND
        elif arr[mid] < target:
            low = mid + 1       ← search right half
        else:
            high = mid - 1      ← search left half

    return -1                   ← NOT FOUND
```

---

## ✏️ Step-by-Step Trace

```
Array: [2, 5, 8, 12, 16, 23, 38, 56, 72, 91]
Index:  0  1  2   3   4   5   6   7   8   9
Target: 23

Step 1: low=0, high=9, mid=4 → arr[4]=16 < 23 → low=5
Step 2: low=5, high=9, mid=7 → arr[7]=56 > 23 → high=6
Step 3: low=5, high=6, mid=5 → arr[5]=23 == 23 → FOUND at index 5 ✅

Total comparisons: 3 (vs 6 for linear search)
```

---

## 📊 Complexity

| Case | Time | Explanation |
|------|------|-------------|
| Best | O(1) | Target is at mid on first try |
| Average | O(log n) | Halving each time |
| Worst | O(log n) | Target not found or at boundary |
| Space | O(1) | Iterative version |

> **Why log n?** If n=1024, you need at most log₂(1024) = 10 comparisons.

---

## ⚖️ Binary Search vs Linear Search

| Feature | Linear Search | Binary Search |
|---------|---------------|---------------|
| Requirement | None | Sorted array |
| Time (worst) | O(n) | O(log n) |
| Time (best) | O(1) | O(1) |
| Works on | Any array | Sorted only |
| Implementation | Simple | Slightly complex |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Using binary search on an **unsorted** array — results are wrong.
> 🚫 **Mistake 2:** Integer overflow in `mid = (low + high) / 2` for large arrays. Use `mid = low + (high - low) / 2`.
> 🚫 **Mistake 3:** Off-by-one errors — condition should be `low <= high`, not `low < high`.

---

## ⚡ One-Minute Recap

- Requires sorted array
- Divide and conquer: check mid, eliminate half
- O(log n) time, O(1) space (iterative)
- 3 cases: found at mid, go right (low=mid+1), go left (high=mid-1)

---

## 📝 Probable Exam Questions

> **5-mark:** Trace binary search for target `72` in array `[5, 12, 23, 38, 56, 72, 91]`. Show each step.
> **Short note:** Why is binary search O(log n)?
> **Conceptual:** What are the preconditions for binary search?

---

---

# 6. Sorting Algorithms

## 💡 Intuition First

> Sorting is like organizing a messy bookshelf. Different strategies exist — some are fast but complex, some are simple but slow. Knowing **which to use when** is the real skill.

---

## 📊 Complexity Comparison Table

| Algorithm | Best | Average | Worst | Space | Stable? |
|-----------|------|---------|-------|-------|---------|
| **Bubble Sort** | O(n) | O(n²) | O(n²) | O(1) | ✅ Yes |
| **Selection Sort** | O(n²) | O(n²) | O(n²) | O(1) | ❌ No |
| **Insertion Sort** | O(n) | O(n²) | O(n²) | O(1) | ✅ Yes |
| **Merge Sort** | O(n log n) | O(n log n) | O(n log n) | O(n) | ✅ Yes |
| **Quick Sort** | O(n log n) | O(n log n) | O(n²) | O(log n) | ❌ No |
| **Heap Sort** | O(n log n) | O(n log n) | O(n log n) | O(1) | ❌ No |

> 🔑 **Memory trick for O(n log n) sorts:** "My Queen Has" → **M**erge, **Q**uick, **H**eap

---

## 🔀 Merge Sort

### Intuition
> Divide the array in half, sort each half, then **merge** the two sorted halves. Like sorting two decks of cards separately, then merging them.

### Algorithm (Divide & Conquer)

```
function mergeSort(arr):
    if len(arr) <= 1: return arr

    mid = len(arr) / 2
    left = mergeSort(arr[0..mid-1])
    right = mergeSort(arr[mid..end])
    return merge(left, right)

function merge(left, right):
    result = []
    i = 0, j = 0
    while i < len(left) AND j < len(right):
        if left[i] <= right[j]:
            result.append(left[i]); i++
        else:
            result.append(right[j]); j++
    append remaining elements
    return result
```

### Trace

```
Array: [38, 27, 43, 3, 9, 82, 10]

DIVIDE:
[38,27,43,3,9,82,10]
    /              \
[38,27,43]      [3,9,82,10]
  /    \           /      \
[38] [27,43]    [3,9]   [82,10]
      / \        / \      / \
    [27][43]   [3] [9] [82][10]

MERGE (bottom up):
[27,43] ← merge [27],[43]
[3,9]   ← merge [3],[9]
[10,82] ← merge [82],[10]
[27,38,43] ← merge [38],[27,43]
[3,9,10,82] ← merge [3,9],[10,82]
[3,9,10,27,38,43,82] ← final merge
```

---

## ⚡ Quick Sort

### Intuition
> Pick a **pivot**. Put all smaller elements to its left, all larger to its right. Recursively sort both sides. The pivot is now in its **final position**.

### Algorithm

```
function quickSort(arr, low, high):
    if low < high:
        pivot_index = partition(arr, low, high)
        quickSort(arr, low, pivot_index - 1)
        quickSort(arr, pivot_index + 1, high)

function partition(arr, low, high):
    pivot = arr[high]   ← last element as pivot
    i = low - 1

    for j = low to high-1:
        if arr[j] <= pivot:
            i++
            swap(arr[i], arr[j])

    swap(arr[i+1], arr[high])
    return i + 1
```

### Trace

```
Array: [10, 80, 30, 90, 40, 50, 70]
Pivot = 70 (last element)

i = -1, j scans left to right:
j=0: arr[0]=10 ≤ 70 → i=0, swap(arr[0],arr[0]) → [10,80,30,90,40,50,70]
j=1: arr[1]=80 > 70 → skip
j=2: arr[2]=30 ≤ 70 → i=1, swap(arr[1],arr[2]) → [10,30,80,90,40,50,70]
j=3: arr[3]=90 > 70 → skip
j=4: arr[4]=40 ≤ 70 → i=2, swap(arr[2],arr[4]) → [10,30,40,90,80,50,70]
j=5: arr[5]=50 ≤ 70 → i=3, swap(arr[3],arr[5]) → [10,30,40,50,80,90,70]

Final: swap(arr[i+1], arr[high]) = swap(arr[4], arr[6])
Result: [10,30,40,50,70,90,80]
                    ↑
               pivot 70 in final position!
```

---

## 🏔️ Heap Sort

### Intuition
> Build a **max-heap** (parent always ≥ children). The root is always the maximum. Extract root, put it at end, re-heapify. Repeat.

### Key Concepts

```
Max-Heap property: parent ≥ children

Array: [4, 10, 3, 5, 1]
As tree:
        [4]
       /   \
     [10]  [3]
     /  \
   [5]  [1]

After heapify:
        [10]
       /    \
     [5]    [3]
     /  \
   [4]  [1]
```

### Algorithm

```
function heapSort(arr):
    n = len(arr)

    // Build max-heap
    for i = n/2 - 1 down to 0:
        heapify(arr, n, i)

    // Extract elements one by one
    for i = n-1 down to 1:
        swap(arr[0], arr[i])    ← move max to end
        heapify(arr, i, 0)      ← re-heapify reduced heap

function heapify(arr, n, i):
    largest = i
    left = 2*i + 1
    right = 2*i + 2

    if left < n AND arr[left] > arr[largest]: largest = left
    if right < n AND arr[right] > arr[largest]: largest = right

    if largest != i:
        swap(arr[i], arr[largest])
        heapify(arr, n, largest)
```

---

## ⚖️ When to Use Which Sort?

| Situation | Best Choice | Why |
|-----------|-------------|-----|
| General purpose | Quick Sort | Fast in practice, O(n log n) avg |
| Guaranteed O(n log n) | Merge Sort | No worst-case degradation |
| In-place, no extra memory | Heap Sort | O(1) space |
| Nearly sorted data | Insertion Sort | O(n) best case |
| Stability required | Merge Sort | Preserves equal element order |
| Small arrays | Insertion Sort | Low overhead |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Quick sort worst case is O(n²) when pivot is always min or max (sorted array with last-element pivot).
> 🚫 **Mistake 2:** Merge sort requires O(n) extra space — it's NOT in-place.
> 🚫 **Mistake 3:** Heap sort is NOT stable — equal elements may change relative order.
> 🚫 **Mistake 4:** Confusing heapify (fix one node) with build-heap (fix entire array).

---

## 🎯 Exam Tips

> 💡 **Most asked:** Merge sort trace, Quick sort partition trace, complexity comparison table.
> 💡 Quick sort pivot selection affects performance — random pivot avoids worst case.
> 💡 Merge sort is preferred for **linked lists** (no random access needed).
> 💡 Heap sort = build max-heap + repeated extraction.

---

## ⚡ One-Minute Recap

- Merge: divide → sort halves → merge | O(n log n) always | O(n) space | stable
- Quick: partition around pivot | O(n log n) avg, O(n²) worst | in-place | not stable
- Heap: build max-heap → extract max | O(n log n) always | O(1) space | not stable

---

## 📝 Probable Exam Questions

> **5-mark:** Trace merge sort on `[38, 27, 43, 3, 9]`. Show divide and merge steps.
> **5-mark:** Trace quick sort partition on `[10, 80, 30, 90, 40, 50, 70]` with last element as pivot.
> **Short note:** Compare merge sort and quick sort.
> **Table:** Fill in the time/space complexity table for all sorting algorithms.

---

---

# 7. Dynamic Programming

## 💡 Intuition First

> You're climbing stairs. At each step, you can go 1 or 2 steps. How many ways to reach step n? Instead of recalculating the same subproblems over and over, **store the results** and reuse them. That's DP.

**Core idea:** Break a problem into **overlapping subproblems**, solve each once, store results (**memoization** or **tabulation**).

**Real-world analogy:** GPS navigation — it doesn't recalculate the entire route from scratch every second. It stores partial results.

**DP vs Greedy:** DP considers ALL possibilities and picks the best. Greedy picks the locally best option at each step.

---

## 📐 Two Approaches

| Approach | Method | Direction |
|----------|--------|-----------|
| **Top-Down (Memoization)** | Recursion + cache | Big → Small |
| **Bottom-Up (Tabulation)** | Iterative table | Small → Big |

---

## 🔢 Example 1: Fibonacci

### Naive Recursion — O(2ⁿ) ❌

```
fib(5) calls fib(4) and fib(3)
fib(4) calls fib(3) and fib(2)
fib(3) is computed TWICE — wasteful!
```

### DP Tabulation — O(n) ✅

```
dp[0] = 0
dp[1] = 1
dp[i] = dp[i-1] + dp[i-2]

i:    0  1  2  3  4  5  6  7
dp:   0  1  1  2  3  5  8  13
```

---

## 🎒 Example 2: 0/1 Knapsack

### Problem

```
Items: weight=[2,3,4,5], value=[3,4,5,6]
Capacity W = 5

Can we take each item at most once?
Maximize total value without exceeding capacity.
```

### DP Table Construction

```
dp[i][w] = max value using first i items with capacity w

Base case: dp[0][w] = 0 for all w (no items)
           dp[i][0] = 0 for all i (no capacity)

Recurrence:
  If weight[i] > w:  dp[i][w] = dp[i-1][w]  (can't take item i)
  Else: dp[i][w] = max(dp[i-1][w],           (don't take item i)
                       dp[i-1][w-weight[i]] + value[i])  (take item i)
```

```
Items: (w=2,v=3), (w=3,v=4), (w=4,v=5), (w=5,v=6)
Capacity = 5

     w=0  w=1  w=2  w=3  w=4  w=5
i=0:  0    0    0    0    0    0
i=1:  0    0    3    3    3    3    ← item1(w=2,v=3)
i=2:  0    0    3    4    4    7    ← item2(w=3,v=4)
i=3:  0    0    3    4    5    7    ← item3(w=4,v=5)
i=4:  0    0    3    4    5    7    ← item4(w=5,v=6)

Answer: dp[4][5] = 7
(Take item1 + item2: weight=2+3=5, value=3+4=7)
```

---

## 📏 Example 3: Longest Common Subsequence (LCS)

### Problem

```
Find the longest subsequence common to both strings.
X = "ABCBDAB"
Y = "BDCAB"
LCS = "BCAB" or "BDAB" → length = 4
```

### DP Table

```
Recurrence:
  If X[i] == Y[j]: dp[i][j] = dp[i-1][j-1] + 1
  Else:            dp[i][j] = max(dp[i-1][j], dp[i][j-1])

     ""  B  D  C  A  B
""    0  0  0  0  0  0
A     0  0  0  0  1  1
B     0  1  1  1  1  2
C     0  1  1  2  2  2
B     0  1  1  2  2  3
D     0  1  2  2  2  3
A     0  1  2  2  3  3
B     0  1  2  2  3  4

LCS length = dp[7][5] = 4
```

---

## ⚖️ DP vs Greedy vs Divide & Conquer

| Feature | DP | Greedy | Divide & Conquer |
|---------|----|---------|--------------------|
| Subproblems | Overlapping | Non-overlapping | Non-overlapping |
| Optimal substructure | ✅ Required | ✅ Required | ✅ Required |
| Approach | All possibilities | Local best | Split & combine |
| Examples | Knapsack, LCS | Activity selection, Huffman | Merge sort, Binary search |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Using DP when subproblems don't overlap — use D&C instead.
> 🚫 **Mistake 2:** In 0/1 knapsack, forgetting the "0/1" constraint — each item used at most once.
> 🚫 **Mistake 3:** LCS ≠ LCS substring. Subsequence doesn't need to be contiguous.
> 🚫 **Mistake 4:** Not initializing base cases (row 0 and column 0) in DP tables.

---

## 🎯 Exam Tips

> 💡 **Knapsack:** Always draw the full DP table. Examiners want to see the table, not just the answer.
> 💡 **LCS:** Trace the table AND backtrack to find the actual subsequence.
> 💡 **Fibonacci:** Show both naive recursion (exponential) and DP (linear) to demonstrate the improvement.
> 💡 DP requires: **optimal substructure** + **overlapping subproblems**.

---

## ⚡ One-Minute Recap

- DP = store subproblem results to avoid recomputation
- Top-down: recursion + memo | Bottom-up: fill table iteratively
- Fibonacci: O(2ⁿ) → O(n) with DP
- Knapsack: dp[i][w] = max value with i items and capacity w
- LCS: dp[i][j] = LCS length of X[1..i] and Y[1..j]

---

## 📝 Probable Exam Questions

> **5-mark:** Solve 0/1 knapsack: items `{(2,3),(3,4),(4,5),(5,6)}`, capacity=5. Show DP table.
> **5-mark:** Find LCS of "AGGTAB" and "GXTXAYB". Show the DP table.
> **Short note:** What is memoization? How does it differ from tabulation?
> **Conceptual:** What are the two properties required for DP to be applicable?

---

---

# 8. Greedy Algorithms

## 💡 Intuition First

> You're at a buffet and can only carry a limited weight. You always pick the **most valuable item per kg** first. That's greedy — make the locally optimal choice at each step, hoping it leads to a globally optimal solution.

**Key insight:** Greedy works when the **greedy choice property** holds — a locally optimal choice leads to a globally optimal solution.

---

## 🗓️ Activity Selection Problem

### Problem

```
Given n activities with start and finish times,
select the maximum number of non-overlapping activities.

Activities: (start, finish)
A1=(1,4), A2=(3,5), A3=(0,6), A4=(5,7), A5=(3,9), A6=(5,9), A7=(6,10), A8=(8,11), A9=(8,12), A10=(2,14), A11=(12,16)
```

### Greedy Strategy

> Sort by **finish time**. Always pick the activity that finishes earliest (leaves most room for future activities).

```
Sorted by finish time:
A1=(1,4), A2=(3,5), A3=(0,6), A4=(5,7), A5=(3,9), A6=(5,9), A7=(6,10), A8=(8,11), A9=(8,12), A10=(2,14), A11=(12,16)

Step 1: Pick A1=(1,4) ← first activity
Step 2: A2=(3,5): start=3 < finish=4 → OVERLAP, skip
Step 3: A3=(0,6): start=0 < finish=4 → OVERLAP, skip
Step 4: A4=(5,7): start=5 ≥ finish=4 → SELECT ✅
Step 5: A5=(3,9): start=3 < finish=7 → OVERLAP, skip
Step 6: A6=(5,9): start=5 < finish=7 → OVERLAP, skip
Step 7: A7=(6,10): start=6 < finish=7 → OVERLAP, skip
Step 8: A8=(8,11): start=8 ≥ finish=7 → SELECT ✅
Step 9: A9=(8,12): start=8 < finish=11 → OVERLAP, skip
Step 10: A10=(2,14): start=2 < finish=11 → OVERLAP, skip
Step 11: A11=(12,16): start=12 ≥ finish=11 → SELECT ✅

Selected: {A1, A4, A8, A11} → 4 activities
```

---

## 🌳 Huffman Coding

### Intuition

> Assign **shorter codes** to more frequent characters. Like Morse code — common letters (E, T) have short codes.

### Algorithm

```
1. Create a leaf node for each character with its frequency
2. Build a min-heap (priority queue) of all nodes
3. Repeat until one node remains:
   a. Extract two nodes with minimum frequency
   b. Create new internal node with frequency = sum of two
   c. Insert new node back into heap
4. The remaining node is the root of the Huffman tree
```

### Trace

```
Characters: a(5), b(9), c(12), d(13), e(16), f(45)

Min-heap: [a:5, b:9, c:12, d:13, e:16, f:45]

Step 1: Extract a:5, b:9 → create node:14
        Heap: [c:12, d:13, node:14, e:16, f:45]

Step 2: Extract c:12, d:13 → create node:25
        Heap: [node:14, e:16, node:25, f:45]

Step 3: Extract node:14, e:16 → create node:30
        Heap: [node:25, node:30, f:45]

Step 4: Extract node:25, node:30 → create node:55
        Heap: [f:45, node:55]

Step 5: Extract f:45, node:55 → create root:100

Huffman Tree:
              [100]
             /     \
          [45:f]  [55]
                  /   \
               [25]   [30]
               /  \   /  \
            [12:c][13:d][14][16:e]
                        /  \
                      [5:a][9:b]

Codes:
f = 0
c = 100
d = 101
a = 1100
b = 1101
e = 111
```

---

## ⚖️ Greedy vs Dynamic Programming

| Feature | Greedy | DP |
|---------|--------|----|
| Choice | Local optimal | All possibilities |
| Subproblems | Non-overlapping | Overlapping |
| Speed | Faster | Slower |
| Correctness | Not always optimal | Always optimal |
| Examples | Activity selection, Huffman | Knapsack, LCS |

> 🔑 **Key:** Fractional knapsack → Greedy ✅ | 0/1 knapsack → DP ✅

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Applying greedy to 0/1 knapsack — it doesn't give optimal results.
> 🚫 **Mistake 2:** In activity selection, sorting by start time (wrong) instead of finish time (correct).
> 🚫 **Mistake 3:** In Huffman, forgetting to re-insert the merged node back into the heap.

---

## ⚡ One-Minute Recap

- Greedy: locally optimal choice at each step
- Activity selection: sort by finish time, pick non-overlapping
- Huffman: build tree from bottom up using min-heap, frequent chars get shorter codes
- Greedy works for: activity selection, Huffman, fractional knapsack, Prim's, Kruskal's, Dijkstra's

---

## 📝 Probable Exam Questions

> **5-mark:** Build a Huffman tree for characters with frequencies: `{a:5, b:9, c:12, d:13, e:16, f:45}`. Find the code for each character.
> **5-mark:** Apply activity selection algorithm to find maximum non-overlapping activities.
> **Short note:** When does greedy fail? Give an example.
> **Conceptual:** What is the greedy choice property?

---

---

# 9. Graph Algorithms

## 💡 Intuition First

> A **graph** is a network — cities connected by roads, people connected by friendships, web pages connected by links. Graph algorithms help us navigate, find shortest paths, and build minimum-cost networks.

---

## 📐 Graph Basics

```
Directed Graph:          Undirected Graph:
  A → B → D               A — B — D
  ↓   ↓                   |   |
  C → E                   C — E
```

| Term | Meaning |
|------|---------|
| **Vertex/Node** | A point in the graph |
| **Edge** | Connection between two vertices |
| **Directed** | Edges have direction (one-way) |
| **Undirected** | Edges are bidirectional |
| **Weighted** | Edges have costs/distances |
| **Adjacent** | Two vertices connected by an edge |
| **Path** | Sequence of vertices connected by edges |
| **Cycle** | Path that starts and ends at same vertex |

---

## 🔍 BFS — Breadth-First Search

### Intuition
> Explore all neighbors at current level before going deeper. Like ripples in water — expand outward layer by layer.

**Uses a QUEUE.**

```
Graph:
    1 — 2 — 5
    |   |
    3 — 4

BFS from vertex 1:

Queue: [1]
Visit 1 → enqueue neighbors 2, 3 → Queue: [2, 3]
Visit 2 → enqueue neighbors 4, 5 → Queue: [3, 4, 5]
Visit 3 → enqueue neighbor 4 (already visited) → Queue: [4, 5]
Visit 4 → no new neighbors → Queue: [5]
Visit 5 → no new neighbors → Queue: []

BFS Order: 1, 2, 3, 4, 5
```

**Pseudocode:**
```
function BFS(graph, start):
    visited = {start}
    queue = [start]

    while queue not empty:
        vertex = queue.dequeue()
        print(vertex)
        for neighbor in graph[vertex]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.enqueue(neighbor)
```

**Applications:** Shortest path (unweighted), level-order traversal, connected components.

---

## 🔍 DFS — Depth-First Search

### Intuition
> Go as deep as possible before backtracking. Like exploring a maze — go down one path until you hit a dead end, then backtrack.

**Uses a STACK (or recursion).**

```
Graph (same as above):
    1 — 2 — 5
    |   |
    3 — 4

DFS from vertex 1 (recursive):

Visit 1 → go to 2
  Visit 2 → go to 4
    Visit 4 → go to 3
      Visit 3 → all neighbors visited, backtrack
    backtrack to 4 → go to 5
      Visit 5 → all neighbors visited, backtrack
    backtrack to 2 → backtrack to 1
  backtrack to 1 → all neighbors visited

DFS Order: 1, 2, 4, 3, 5
```

**Applications:** Cycle detection, topological sort, connected components, maze solving.

---

## ⚖️ BFS vs DFS

| Feature | BFS | DFS |
|---------|-----|-----|
| Data structure | Queue | Stack / Recursion |
| Traversal | Level by level | Deep first |
| Shortest path | ✅ (unweighted) | ❌ |
| Memory | O(w) — width | O(h) — height |
| Cycle detection | ✅ | ✅ |
| Topological sort | ❌ | ✅ |

---

## 🗺️ Dijkstra's Algorithm (Shortest Path)

### Intuition
> Find the shortest path from a source to all other vertices. Like a GPS — always extend the currently shortest known path.

**Works on weighted graphs with NON-NEGATIVE weights.**

```
Graph:
    A --4-- B
    |       |
    2       1
    |       |
    C --3-- D --5-- E

Find shortest path from A to all vertices.

Initial: dist = {A:0, B:∞, C:∞, D:∞, E:∞}
Visited = {}

Step 1: Pick A (dist=0), mark visited
  Update: B = min(∞, 0+4) = 4
          C = min(∞, 0+2) = 2
  dist = {A:0, B:4, C:2, D:∞, E:∞}

Step 2: Pick C (dist=2, minimum unvisited), mark visited
  Update: D = min(∞, 2+3) = 5
  dist = {A:0, B:4, C:2, D:5, E:∞}

Step 3: Pick B (dist=4), mark visited
  Update: D = min(5, 4+1) = 5 (no change)
  dist = {A:0, B:4, C:2, D:5, E:∞}

Step 4: Pick D (dist=5), mark visited
  Update: E = min(∞, 5+5) = 10
  dist = {A:0, B:4, C:2, D:5, E:10}

Step 5: Pick E (dist=10), mark visited

Final shortest distances from A:
  A=0, B=4, C=2, D=5, E=10
```

---

## 🌲 Minimum Spanning Tree

### Prim's Algorithm

> Start from any vertex. Always add the **cheapest edge** connecting the current tree to a new vertex.

```
Graph:
  A --4-- B
  |  \    |
  2   3   1
  |    \  |
  C --5-- D

Start from A:
Step 1: Add A. Edges from A: (A-C,2), (A-D,3), (A-B,4)
Step 2: Pick cheapest: A-C (cost 2). Add C.
        Edges: (A-D,3), (A-B,4), (C-D,5)
Step 3: Pick cheapest: A-D (cost 3). Add D.
        Edges: (A-B,4), (D-B,1), (C-D,5)
Step 4: Pick cheapest: D-B (cost 1). Add B.

MST edges: {A-C, A-D, D-B}
MST cost: 2+3+1 = 6
```

### Kruskal's Algorithm

> Sort ALL edges by weight. Add edges one by one (cheapest first) if they don't create a cycle.

```
Edges sorted: (D-B,1), (A-C,2), (A-D,3), (A-B,4), (C-D,5)

Step 1: Add D-B (1) → no cycle ✅
Step 2: Add A-C (2) → no cycle ✅
Step 3: Add A-D (3) → no cycle ✅
Step 4: Add A-B (4) → creates cycle A-D-B-A ❌ skip
Step 5: Add C-D (5) → creates cycle ❌ skip

MST: {D-B, A-C, A-D}, cost = 6
```

### Prim's vs Kruskal's

| Feature | Prim's | Kruskal's |
|---------|--------|-----------|
| Approach | Grow from one vertex | Add cheapest edge globally |
| Data structure | Priority queue | Union-Find |
| Best for | Dense graphs | Sparse graphs |
| Complexity | O(E log V) | O(E log E) |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Dijkstra fails with **negative weights** — use Bellman-Ford instead.
> 🚫 **Mistake 2:** BFS gives shortest path only for **unweighted** graphs.
> 🚫 **Mistake 3:** In Kruskal's, forgetting to check for cycles (use Union-Find).
> 🚫 **Mistake 4:** Confusing MST (minimum spanning tree) with shortest path — they're different problems.

---

## 🎯 Exam Tips

> 💡 **BFS = Queue | DFS = Stack** — always state this.
> 💡 Dijkstra: always pick the **minimum distance unvisited** vertex next.
> 💡 Kruskal's: sort edges, add if no cycle. Prim's: grow tree greedily.
> 💡 Be ready to trace BFS/DFS on a given graph and write the traversal order.

---

## ⚡ One-Minute Recap

- BFS: queue, level-by-level, shortest path (unweighted)
- DFS: stack/recursion, deep first, topological sort
- Dijkstra: shortest path, weighted, non-negative edges
- Prim's: MST, grow from one vertex
- Kruskal's: MST, sort edges, add if no cycle

---

## 📝 Probable Exam Questions

> **5-mark:** Apply Dijkstra's algorithm on a given weighted graph. Show all steps and final distances.
> **5-mark:** Find the MST using Kruskal's algorithm. Show edge selection steps.
> **Short note:** Compare BFS and DFS with examples.
> **Trace:** Perform BFS and DFS on a given graph starting from vertex A. Write traversal order.

---

---

# 10. Complexity Analysis

## 💡 Intuition First

> How does your algorithm **scale** as input grows? If n doubles, does your program take 2x longer? 4x? 2ⁿ times? Complexity analysis answers this — without running the code.

**Real-world analogy:** Searching a name in a list of 10 vs 10 million people. Linear search: 10x harder. Binary search: barely harder (log₂ of 10M ≈ 23 steps).

---

## 📐 Big-O Notation

> Big-O describes the **upper bound** — worst-case growth rate, ignoring constants and lower-order terms.

```
f(n) = 3n² + 5n + 100
Big-O: O(n²)   ← dominant term, drop constants
```

### Common Complexities (Best to Worst)

```
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ) < O(n!)
```

| Notation | Name | Example |
|----------|------|---------|
| O(1) | Constant | Array access, hash lookup |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Linear search, traversal |
| O(n log n) | Linearithmic | Merge sort, heap sort |
| O(n²) | Quadratic | Bubble sort, nested loops |
| O(2ⁿ) | Exponential | Naive Fibonacci, subset generation |
| O(n!) | Factorial | Permutations, brute-force TSP |

---

## 📊 Best / Average / Worst Case

```
Example: Linear search in array of n elements

Best case:    Target is at index 0 → O(1)
Average case: Target is in the middle → O(n/2) = O(n)
Worst case:   Target is at last index or not found → O(n)
```

| Notation | Meaning |
|----------|---------|
| **O (Big-O)** | Upper bound (worst case) |
| **Ω (Omega)** | Lower bound (best case) |
| **Θ (Theta)** | Tight bound (average case) |

---

## 🔁 Recurrence Relations

> Used to express the time complexity of recursive algorithms.

### Common Recurrences

| Algorithm | Recurrence | Solution |
|-----------|------------|----------|
| Binary Search | T(n) = T(n/2) + O(1) | O(log n) |
| Merge Sort | T(n) = 2T(n/2) + O(n) | O(n log n) |
| Quick Sort (avg) | T(n) = 2T(n/2) + O(n) | O(n log n) |
| Naive Fibonacci | T(n) = T(n-1) + T(n-2) | O(2ⁿ) |

---

## 🏛️ Master Theorem

> A shortcut for solving recurrences of the form: **T(n) = aT(n/b) + f(n)**

```
Where:
  a = number of subproblems
  b = factor by which input is divided
  f(n) = work done outside recursive calls

Compare f(n) with n^(log_b(a)):

Case 1: f(n) = O(n^(log_b(a) - ε))  → T(n) = Θ(n^log_b(a))
Case 2: f(n) = Θ(n^log_b(a))        → T(n) = Θ(n^log_b(a) · log n)
Case 3: f(n) = Ω(n^(log_b(a) + ε))  → T(n) = Θ(f(n))
```

### Examples

```
Merge Sort: T(n) = 2T(n/2) + n
  a=2, b=2, f(n)=n
  n^(log_2(2)) = n^1 = n
  f(n) = n = Θ(n^1) → Case 2
  T(n) = Θ(n log n) ✅

Binary Search: T(n) = T(n/2) + 1
  a=1, b=2, f(n)=1
  n^(log_2(1)) = n^0 = 1
  f(n) = 1 = Θ(1) → Case 2
  T(n) = Θ(log n) ✅
```

---

## 📊 Algorithm Complexity Quick Reference

| Algorithm | Time (Best) | Time (Avg) | Time (Worst) | Space |
|-----------|-------------|------------|--------------|-------|
| Linear Search | O(1) | O(n) | O(n) | O(1) |
| Binary Search | O(1) | O(log n) | O(log n) | O(1) |
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) |
| Heap Sort | O(n log n) | O(n log n) | O(n log n) | O(1) |
| BST Search | O(1) | O(log n) | O(n) | — |
| BFS/DFS | — | O(V+E) | O(V+E) | O(V) |
| Dijkstra | — | O(E log V) | O(E log V) | O(V) |
| Kruskal's | — | O(E log E) | O(E log E) | O(V) |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Saying O(2n) instead of O(n) — always drop constants.
> 🚫 **Mistake 2:** Confusing O (worst) with Ω (best) — Big-O is NOT always worst case by definition, but it's commonly used that way.
> 🚫 **Mistake 3:** Nested loops don't always mean O(n²) — check if inner loop depends on outer.
> 🚫 **Mistake 4:** Forgetting space complexity — recursive algorithms use O(n) stack space.

---

## 🎯 Exam Tips

> 💡 **Master Theorem** is a high-frequency exam topic — memorize the 3 cases.
> 💡 Always simplify: O(3n² + 5n + 100) = O(n²).
> 💡 Quick sort worst case is O(n²) — when pivot is always min or max.
> 💡 BST worst case is O(n) — when tree is completely skewed (like a linked list).

---

## ⚡ One-Minute Recap

- Big-O = upper bound, drop constants and lower terms
- O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ)
- Master theorem: T(n) = aT(n/b) + f(n) → compare f(n) with n^log_b(a)
- Merge sort: O(n log n) always | Quick sort: O(n²) worst | Binary search: O(log n)

---

## 📝 Probable Exam Questions

> **5-mark:** Solve the recurrence T(n) = 2T(n/2) + n using the Master Theorem.
> **5-mark:** What is the time complexity of the following code? Justify.
> **Short note:** Explain Big-O, Big-Omega, and Big-Theta with examples.
> **Table:** Fill in best/average/worst case complexities for merge sort, quick sort, and heap sort.

---

---

# 🏁 Master Quick Revision Sheet — DSA

## ⚡ Complexity Cheat Sheet

```
Data Structure Operations:
┌─────────────────┬──────────┬──────────┬──────────┐
│ Structure       │ Access   │ Search   │ Insert   │
├─────────────────┼──────────┼──────────┼──────────┤
│ Array           │ O(1)     │ O(n)     │ O(n)     │
│ Linked List     │ O(n)     │ O(n)     │ O(1)*    │
│ Stack/Queue     │ O(n)     │ O(n)     │ O(1)     │
│ BST (balanced)  │ O(log n) │ O(log n) │ O(log n) │
│ Hash Table      │ O(1)     │ O(1)     │ O(1)     │
└─────────────────┴──────────┴──────────┴──────────┘
* Insert at head
```

## 🔑 Key Facts to Remember

| Fact | Detail |
|------|--------|
| Inorder BST | Gives sorted output |
| BFS uses | Queue |
| DFS uses | Stack / Recursion |
| Dijkstra fails | Negative weights |
| Stable sorts | Merge, Bubble, Insertion |
| In-place sorts | Heap, Quick, Bubble |
| DP requires | Optimal substructure + overlapping subproblems |
| Greedy works | Activity selection, Huffman, fractional knapsack |
| Master theorem | T(n) = aT(n/b) + f(n) |
| Quick sort worst | O(n²) — sorted input with bad pivot |

## 🧠 Memory Tricks

- **Traversals:** "**P**re = **P**arents first | **In** = **In** order (sorted) | **Post** = **P**arents last"
- **Sorting O(n log n):** "**M**y **Q**ueen **H**as" → Merge, Quick, Heap
- **Greedy vs DP:** "Greedy is **selfish** (local best) | DP is **thorough** (all options)"
- **Stack vs Queue:** "Stack = **S**ame end | Queue = **Q**ueue at different ends"
- **Chaining vs Open:** "**C**haining = **C**hain (linked list) | **O**pen addressing = **O**pen slots"

## 🎯 Top 10 Most Probable Exam Questions

1. Trace binary search on a given array
2. Insert elements into BST and write inorder traversal
3. Reverse a linked list — algorithm + trace
4. Merge sort trace — divide and merge steps
5. Quick sort partition trace
6. Solve 0/1 knapsack with DP table
7. Find LCS of two strings with DP table
8. Apply Dijkstra's algorithm on weighted graph
9. Find MST using Kruskal's or Prim's
10. Solve recurrence using Master Theorem

---

> 📌 **End of Subject 01: Data Structures & Algorithms**
> 
> Next: **Subject 02 — Operating Systems** →

---

*Handbook generated for MSc Admission Preparation | JUST-Style Exam Focus*
*Version 1.0 | Data Structures & Algorithms*
