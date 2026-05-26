# 📘 MSc Admission Prep — Subject 10: Programming Fundamentals
### 🎯 JUST-Style Exam Handbook | Fast Revision Edition

> **Goal:** Exam-focused revision of pseudocode, control structures, arrays, functions, and problem-solving patterns. Every topic includes traces, worked examples, and exam tips.

---

## 📋 Table of Contents

| # | Topic | Tier |
|---|-------|------|
| 1 | [Pseudocode Writing](#1-pseudocode-writing) | 🔴 Must Master |
| 2 | [Loops](#2-loops) | 🔴 Must Master |
| 3 | [Conditionals](#3-conditionals) | 🔴 Must Master |
| 4 | [Arrays](#4-arrays) | 🔴 Must Master |
| 5 | [Functions](#5-functions) | 🔴 Must Master |
| 6 | [Coordinate Movement Problems](#6-coordinate-movement-problems) | 🔴 Must Master |
| 7 | [Pattern & Problem-Solving Algorithms](#7-pattern--problem-solving-algorithms) | 🔴 Must Master |

---

---

# 1. Pseudocode Writing

## 💡 Intuition First

> Pseudocode is **plain-English code** — it describes an algorithm's logic without worrying about syntax. It's the bridge between human thinking and actual code. Examiners love it because it tests whether you understand the logic, not whether you remember Java syntax.

**Real-world analogy:** A recipe is pseudocode for cooking — "Add 2 cups flour, mix until smooth" describes the steps without specifying which brand of bowl to use.

---

## 📐 Pseudocode Conventions

```
Standard keywords (use consistently):
  START / END          → begin and end of algorithm
  INPUT / READ         → get input from user
  OUTPUT / PRINT       → display output
  SET / LET            → assign a value
  IF / THEN / ELSE / ENDIF → conditional
  WHILE / DO / ENDWHILE → while loop
  FOR / TO / STEP / ENDFOR → for loop
  REPEAT / UNTIL       → do-while loop
  FUNCTION / RETURN    → define and return from function
  CALL                 → invoke a function
  AND / OR / NOT       → logical operators
  ← or =              → assignment
```

---

## 📐 Pseudocode Structure

```
Algorithm: Find Maximum of Two Numbers

START
  INPUT a, b
  IF a > b THEN
    SET max ← a
  ELSE
    SET max ← b
  ENDIF
  OUTPUT "Maximum is: ", max
END
```

---

## ✏️ Worked Examples

### Example 1: Sum of N Numbers

```
Algorithm: Sum of first N natural numbers

START
  INPUT n
  SET sum ← 0
  SET i ← 1
  WHILE i <= n DO
    SET sum ← sum + i
    SET i ← i + 1
  ENDWHILE
  OUTPUT "Sum = ", sum
END

Trace for n=4:
  i=1: sum=0+1=1
  i=2: sum=1+2=3
  i=3: sum=3+3=6
  i=4: sum=6+4=10
  i=5: 5>4, exit loop
  Output: Sum = 10
```

### Example 2: Check Prime Number

```
Algorithm: Check if n is prime

START
  INPUT n
  IF n <= 1 THEN
    OUTPUT "Not prime"
    STOP
  ENDIF
  SET isPrime ← TRUE
  SET i ← 2
  WHILE i <= sqrt(n) DO
    IF n MOD i = 0 THEN
      SET isPrime ← FALSE
      BREAK
    ENDIF
    SET i ← i + 1
  ENDWHILE
  IF isPrime = TRUE THEN
    OUTPUT n, " is prime"
  ELSE
    OUTPUT n, " is not prime"
  ENDIF
END
```

### Example 3: Factorial (Recursive)

```
FUNCTION factorial(n)
  IF n = 0 OR n = 1 THEN
    RETURN 1
  ELSE
    RETURN n * factorial(n - 1)
  ENDIF
END FUNCTION

Trace for factorial(4):
  factorial(4) = 4 × factorial(3)
               = 4 × 3 × factorial(2)
               = 4 × 3 × 2 × factorial(1)
               = 4 × 3 × 2 × 1
               = 24
```

---

## 📐 Pseudocode Quality Checklist

```
✅ Clear variable names (not x, y — use meaningful names)
✅ Consistent indentation (shows structure)
✅ Every loop has a clear termination condition
✅ Every IF has a matching ENDIF
✅ Input and output clearly labeled
✅ Edge cases handled (n=0, empty array, etc.)
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Using actual programming syntax (semicolons, curly braces) — pseudocode should be language-agnostic.
> 🚫 **Mistake 2:** Forgetting to initialize variables before using them.
> 🚫 **Mistake 3:** Off-by-one errors in loop bounds (use `<=` vs `<` carefully).
> 🚫 **Mistake 4:** Not showing the trace — examiners want to see step-by-step execution.

---

## ⚡ One-Minute Recap

- Pseudocode: algorithm in plain English, language-independent
- Key keywords: INPUT, OUTPUT, IF/THEN/ELSE, WHILE, FOR, FUNCTION, RETURN
- Always trace your pseudocode with a sample input
- Indentation shows structure (loop body, if body)

---

## 📝 Probable Exam Questions

> **5-mark:** Write pseudocode to find the largest element in an array of n numbers.
> **5-mark:** Write pseudocode for bubble sort. Trace it on [5, 3, 8, 1].
> **Write:** Write pseudocode to check if a string is a palindrome.
> **Trace:** Trace the given pseudocode with input n=5 and show all variable values.

---

---

# 2. Loops

## 💡 Intuition First

> Loops let you **repeat a block of code** without writing it multiple times. Like a washing machine cycle — it keeps spinning until the clothes are clean (condition met).

---

## 📐 For Loop

> Use when you know **exactly how many times** to repeat.

```
Pseudocode:
FOR i ← 1 TO n STEP 1 DO
  [body]
ENDFOR

Java:
for (int i = 1; i <= n; i++) {
  // body
}

Python:
for i in range(1, n+1):
  # body
```

### Trace: Print 1 to 5

```
FOR i ← 1 TO 5 DO
  OUTPUT i
ENDFOR

Trace:
  i=1: output 1
  i=2: output 2
  i=3: output 3
  i=4: output 4
  i=5: output 5
  i=6: 6>5, exit
Output: 1 2 3 4 5
```

---

## 📐 While Loop

> Use when you repeat **while a condition is true** (don't know exact count).

```
Pseudocode:
WHILE condition DO
  [body]
ENDWHILE

Java:
while (condition) {
  // body
}
```

### Trace: Sum until user enters 0

```
SET sum ← 0
INPUT num
WHILE num ≠ 0 DO
  SET sum ← sum + num
  INPUT num
ENDWHILE
OUTPUT sum

Trace (inputs: 3, 5, 2, 0):
  sum=0, num=3
  sum=3, num=5
  sum=8, num=2
  sum=10, num=0 → exit
Output: 10
```

---

## 📐 Do-While Loop (Repeat-Until)

> Execute body **at least once**, then check condition.

```
Pseudocode:
REPEAT
  [body]
UNTIL condition

Java:
do {
  // body
} while (condition);
```

### Trace: Input validation

```
REPEAT
  INPUT age
  IF age < 0 OR age > 150 THEN
    OUTPUT "Invalid age, try again"
  ENDIF
UNTIL age >= 0 AND age <= 150

Trace (inputs: -5, 200, 25):
  age=-5:  invalid, repeat
  age=200: invalid, repeat
  age=25:  valid, exit
```

---

## 📐 Nested Loops

```
FOR i ← 1 TO 3 DO
  FOR j ← 1 TO 3 DO
    OUTPUT i, " × ", j, " = ", i*j
  ENDFOR
ENDFOR

Trace:
  i=1: j=1→1×1=1, j=2→1×2=2, j=3→1×3=3
  i=2: j=1→2×1=2, j=2→2×2=4, j=3→2×3=6
  i=3: j=1→3×1=3, j=2→3×2=6, j=3→3×3=9

Total iterations: 3 × 3 = 9
```

---

## ⚖️ Loop Comparison

| Loop | Use When | Executes at Least Once? |
|------|----------|------------------------|
| `for` | Known number of iterations | Depends on condition |
| `while` | Unknown iterations, check first | No (if condition false initially) |
| `do-while` | Must execute at least once | Yes |

---

## 📐 Loop Control Statements

```
BREAK:    Exit the loop immediately
CONTINUE: Skip rest of current iteration, go to next

Example — print odd numbers 1-10:
FOR i ← 1 TO 10 DO
  IF i MOD 2 = 0 THEN
    CONTINUE    ← skip even numbers
  ENDIF
  OUTPUT i
ENDFOR
Output: 1 3 5 7 9

Example — find first negative:
FOR i ← 0 TO n-1 DO
  IF arr[i] < 0 THEN
    OUTPUT "First negative at index ", i
    BREAK       ← stop searching
  ENDIF
ENDFOR
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Infinite loop — forgetting to update the loop variable (`i++` missing).
> 🚫 **Mistake 2:** Off-by-one — `i < n` vs `i <= n` — know which you need.
> 🚫 **Mistake 3:** Modifying loop variable inside the loop body (confusing behavior).
> 🚫 **Mistake 4:** Nested loop complexity — two nested loops over n = O(n²).

---

## ⚡ One-Minute Recap

- for: known count | while: unknown count, check first | do-while: at least once
- break: exit loop | continue: skip to next iteration
- Nested loops: O(n²) for two loops over n
- Always ensure loop terminates (update condition variable)

---

## 📝 Probable Exam Questions

> **Trace:** Trace the given loop with specific input values. Show all variable states.
> **Write:** Write pseudocode using a while loop to find the GCD of two numbers.
> **Identify:** What is the output of the given nested loop code?

---

---

# 3. Conditionals

## 💡 Intuition First

> Conditionals let your program **make decisions** — "if this is true, do that; otherwise, do something else." Like a traffic light — if red, stop; if green, go; if yellow, slow down.

---

## 📐 If-Else

```
Pseudocode:
IF condition THEN
  [statements if true]
ELSE
  [statements if false]
ENDIF

Java:
if (condition) {
  // true branch
} else {
  // false branch
}
```

### Nested If-Else (Grade Example)

```
INPUT marks
IF marks >= 90 THEN
  OUTPUT "A"
ELSE IF marks >= 80 THEN
  OUTPUT "B"
ELSE IF marks >= 70 THEN
  OUTPUT "C"
ELSE IF marks >= 60 THEN
  OUTPUT "D"
ELSE
  OUTPUT "F"
ENDIF

Trace for marks=75:
  75 >= 90? No
  75 >= 80? No
  75 >= 70? Yes → Output "C"
```

---

## 📐 Switch/Case

> Use when comparing one variable against multiple specific values.

```
Pseudocode:
SWITCH day
  CASE 1: OUTPUT "Monday"
  CASE 2: OUTPUT "Tuesday"
  CASE 3: OUTPUT "Wednesday"
  ...
  DEFAULT: OUTPUT "Invalid day"
ENDSWITCH

Java:
switch (day) {
  case 1: System.out.println("Monday"); break;
  case 2: System.out.println("Tuesday"); break;
  default: System.out.println("Invalid");
}
```

---

## 📐 Logical Operators in Conditions

```
AND: both conditions must be true
  IF age >= 18 AND hasID = TRUE THEN
    OUTPUT "Can enter"
  ENDIF

OR: at least one condition must be true
  IF score >= 90 OR extraCredit = TRUE THEN
    OUTPUT "Grade A"
  ENDIF

NOT: negate a condition
  IF NOT (isLoggedIn) THEN
    OUTPUT "Please login"
  ENDIF

Short-circuit evaluation:
  AND: if first is false, second not evaluated
  OR:  if first is true, second not evaluated
```

---

## 📐 Ternary / Conditional Expression

```
Java:
  result = (condition) ? valueIfTrue : valueIfFalse;

  int max = (a > b) ? a : b;
  String grade = (score >= 60) ? "Pass" : "Fail";

Pseudocode equivalent:
  IF a > b THEN max ← a ELSE max ← b ENDIF
```

---

## ✏️ Worked Example: Leap Year Check

```
Algorithm: Check if year is a leap year

A year is a leap year if:
  (divisible by 4) AND (NOT divisible by 100)
  OR (divisible by 400)

START
  INPUT year
  IF (year MOD 400 = 0) THEN
    OUTPUT year, " is a leap year"
  ELSE IF (year MOD 100 = 0) THEN
    OUTPUT year, " is NOT a leap year"
  ELSE IF (year MOD 4 = 0) THEN
    OUTPUT year, " is a leap year"
  ELSE
    OUTPUT year, " is NOT a leap year"
  ENDIF
END

Trace:
  year=2000: 2000 MOD 400 = 0 → leap year ✅
  year=1900: 1900 MOD 400 ≠ 0, 1900 MOD 100 = 0 → NOT leap year ✅
  year=2024: 2024 MOD 400 ≠ 0, 2024 MOD 100 ≠ 0, 2024 MOD 4 = 0 → leap year ✅
  year=2023: none match → NOT leap year ✅
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Using `=` (assignment) instead of `==` (comparison) in conditions.
> 🚫 **Mistake 2:** Forgetting `break` in switch-case → fall-through to next case.
> 🚫 **Mistake 3:** Order matters in if-else chains — more specific conditions first.
> 🚫 **Mistake 4:** Floating-point comparison: `if (x == 0.1)` is unreliable — use `Math.abs(x - 0.1) < epsilon`.

---

## ⚡ One-Minute Recap

- if-else: binary decision | if-else if-else: multiple conditions
- switch: compare one variable to multiple values
- AND: both true | OR: either true | NOT: negate
- Order matters: check specific conditions before general ones

---

## 📝 Probable Exam Questions

> **Write:** Write pseudocode to classify a triangle as equilateral, isosceles, or scalene.
> **Trace:** Trace the given if-else chain for input x=75.
> **Write:** Write pseudocode to find the maximum of three numbers using conditionals.

---

---

# 4. Arrays

## 💡 Intuition First

> An **array** is a collection of elements of the **same type** stored in **contiguous memory**, accessed by index. Like a row of numbered lockers — locker 0, locker 1, locker 2... you access any locker directly by its number.

---

## 📐 Array Basics

```
Declaration and initialization:
  int[] arr = {5, 3, 8, 1, 9, 2};
  Index:       0  1  2  3  4  5

  arr[0] = 5  (first element)
  arr[5] = 2  (last element)
  arr.length = 6

Memory layout:
  Address: 100  104  108  112  116  120
  Value:     5    3    8    1    9    2
  Index:     0    1    2    3    4    5
  (each int = 4 bytes, contiguous)
```

---

## 📐 Common Array Operations

### Linear Search

```
FUNCTION linearSearch(arr, n, target)
  FOR i ← 0 TO n-1 DO
    IF arr[i] = target THEN
      RETURN i    ← found at index i
    ENDIF
  ENDFOR
  RETURN -1       ← not found

Trace: arr=[5,3,8,1,9], target=8
  i=0: arr[0]=5 ≠ 8
  i=1: arr[1]=3 ≠ 8
  i=2: arr[2]=8 = 8 → return 2 ✅
Time: O(n)
```

### Find Maximum

```
FUNCTION findMax(arr, n)
  SET max ← arr[0]
  FOR i ← 1 TO n-1 DO
    IF arr[i] > max THEN
      SET max ← arr[i]
    ENDIF
  ENDFOR
  RETURN max

Trace: arr=[5,3,8,1,9]
  max=5
  i=1: 3>5? No
  i=2: 8>5? Yes → max=8
  i=3: 1>8? No
  i=4: 9>8? Yes → max=9
  Return 9 ✅
```

### Reverse an Array

```
FUNCTION reverse(arr, n)
  SET left ← 0
  SET right ← n-1
  WHILE left < right DO
    SWAP arr[left] and arr[right]
    SET left ← left + 1
    SET right ← right - 1
  ENDWHILE

Trace: arr=[1,2,3,4,5]
  left=0,right=4: swap arr[0]↔arr[4] → [5,2,3,4,1]
  left=1,right=3: swap arr[1]↔arr[3] → [5,4,3,2,1]
  left=2,right=2: 2<2 false → stop
  Result: [5,4,3,2,1] ✅
```

### Bubble Sort (Array)

```
FUNCTION bubbleSort(arr, n)
  FOR i ← 0 TO n-2 DO
    FOR j ← 0 TO n-2-i DO
      IF arr[j] > arr[j+1] THEN
        SWAP arr[j] and arr[j+1]
      ENDIF
    ENDFOR
  ENDFOR

Trace: arr=[5,3,8,1]
Pass 1 (i=0):
  j=0: 5>3? Yes → [3,5,8,1]
  j=1: 5>8? No
  j=2: 8>1? Yes → [3,5,1,8]
Pass 2 (i=1):
  j=0: 3>5? No
  j=1: 5>1? Yes → [3,1,5,8]
Pass 3 (i=2):
  j=0: 3>1? Yes → [1,3,5,8]
Result: [1,3,5,8] ✅
```

---

## 📐 2D Arrays (Matrix)

```
Declaration:
  int[][] matrix = new int[3][4];  // 3 rows, 4 columns

  matrix[row][col]
  matrix[0][0] = top-left
  matrix[2][3] = bottom-right

Traversal:
FOR i ← 0 TO rows-1 DO
  FOR j ← 0 TO cols-1 DO
    OUTPUT matrix[i][j]
  ENDFOR
ENDFOR

Matrix addition:
FOR i ← 0 TO n-1 DO
  FOR j ← 0 TO m-1 DO
    result[i][j] ← A[i][j] + B[i][j]
  ENDFOR
ENDFOR
```

---

## 📐 Array vs ArrayList

| Feature | Array | ArrayList |
|---------|-------|-----------|
| Size | Fixed at creation | Dynamic (grows/shrinks) |
| Type | Primitive or object | Objects only |
| Access | O(1) by index | O(1) by index |
| Insert/Delete | O(n) (shift elements) | O(n) (shift elements) |
| Memory | Contiguous | May reallocate |
| Syntax | `arr[i]` | `list.get(i)` |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Array index starts at 0, not 1. Last element is at index `n-1`.
> 🚫 **Mistake 2:** `ArrayIndexOutOfBoundsException` — accessing index ≥ length.
> 🚫 **Mistake 3:** In bubble sort inner loop: `j < n-1-i` (not `j < n-1`) — optimization.
> 🚫 **Mistake 4:** 2D array: `matrix[row][col]` — row first, column second.

---

## ⚡ One-Minute Recap

- Array: fixed size, same type, O(1) access by index
- Index: 0 to n-1 | Last element: arr[n-1]
- Linear search: O(n) | Binary search: O(log n) (sorted only)
- Bubble sort: O(n²) | Reverse: O(n) with two pointers
- 2D array: matrix[row][col], nested loops for traversal

---

## 📝 Probable Exam Questions

> **5-mark:** Write pseudocode for bubble sort. Trace it on [4, 2, 7, 1, 5].
> **Write:** Write pseudocode to find the second largest element in an array.
> **Trace:** Trace the reverse array algorithm on [1, 2, 3, 4, 5].
> **Write:** Write pseudocode to count occurrences of a value in an array.

---

---

# 5. Functions

## 💡 Intuition First

> A **function** is a named, reusable block of code that performs a specific task. Instead of writing the same code 10 times, write it once as a function and call it 10 times. Like a recipe — write it once, cook it many times.

**Why functions matter:** Code reuse, modularity, readability, easier testing and debugging.

---

## 📐 Function Anatomy

```
FUNCTION functionName(parameter1, parameter2, ...)
  [function body]
  RETURN value
END FUNCTION

Components:
  Name:       Identifies the function
  Parameters: Input values (formal parameters)
  Body:       The code that executes
  Return:     Output value (or void if none)
  Call:       CALL functionName(arg1, arg2)
              or result ← functionName(arg1, arg2)
```

---

## 📐 Function Examples

### Simple Function

```
FUNCTION square(n)
  RETURN n * n
END FUNCTION

FUNCTION cube(n)
  RETURN n * n * n
END FUNCTION

// Usage:
OUTPUT square(5)    → 25
OUTPUT cube(3)      → 27
OUTPUT square(cube(2))  → square(8) → 64
```

### Function with Multiple Parameters

```
FUNCTION max(a, b, c)
  SET result ← a
  IF b > result THEN SET result ← b ENDIF
  IF c > result THEN SET result ← c ENDIF
  RETURN result
END FUNCTION

Trace: max(3, 7, 5)
  result = 3
  7 > 3? Yes → result = 7
  5 > 7? No
  Return 7 ✅
```

### Void Function (No Return Value)

```
FUNCTION printStars(n)
  FOR i ← 1 TO n DO
    OUTPUT "*"
  ENDFOR
  OUTPUT newline
END FUNCTION

CALL printStars(5)  → *****
```

---

## 📐 Recursion

> A function that **calls itself**. Must have a base case (stopping condition) and a recursive case.

```
FUNCTION factorial(n)
  IF n = 0 OR n = 1 THEN    ← base case
    RETURN 1
  ELSE
    RETURN n * factorial(n-1)  ← recursive case
  ENDIF
END FUNCTION

Call stack for factorial(4):
  factorial(4)
    → 4 * factorial(3)
         → 3 * factorial(2)
              → 2 * factorial(1)
                   → return 1
              → return 2 * 1 = 2
         → return 3 * 2 = 6
    → return 4 * 6 = 24
```

### Fibonacci (Recursive)

```
FUNCTION fib(n)
  IF n = 0 THEN RETURN 0
  IF n = 1 THEN RETURN 1
  RETURN fib(n-1) + fib(n-2)
END FUNCTION

fib(5) = fib(4) + fib(3)
       = (fib(3)+fib(2)) + (fib(2)+fib(1))
       = ((fib(2)+fib(1))+(fib(1)+fib(0))) + ((fib(1)+fib(0))+1)
       = ((1+1+1+0) + (1+0+1))
       = 5

Note: Naive recursion is O(2ⁿ) — use DP for efficiency
```

---

## 📐 Pass by Value vs Pass by Reference

```
Pass by Value (Java primitives):
  A COPY of the value is passed
  Changes inside function don't affect original

  FUNCTION addTen(x)
    x ← x + 10    ← modifies local copy only
    RETURN x
  END FUNCTION

  a ← 5
  CALL addTen(a)
  OUTPUT a    → still 5 (original unchanged)

Pass by Reference (Java objects/arrays):
  The REFERENCE (address) is passed
  Changes inside function DO affect original

  FUNCTION doubleAll(arr, n)
    FOR i ← 0 TO n-1 DO
      arr[i] ← arr[i] * 2    ← modifies original array!
    ENDFOR
  END FUNCTION

  arr = [1, 2, 3]
  CALL doubleAll(arr, 3)
  OUTPUT arr    → [2, 4, 6] (original changed!)
```

---

## ⚖️ Iteration vs Recursion

| Feature | Iteration | Recursion |
|---------|-----------|-----------|
| Mechanism | Loop | Function calls itself |
| Memory | O(1) extra | O(n) call stack |
| Speed | Generally faster | Overhead of function calls |
| Readability | Sometimes verbose | Often elegant |
| Risk | Infinite loop | Stack overflow |
| Best for | Simple repetition | Tree/graph traversal, divide & conquer |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Recursion without base case → infinite recursion → stack overflow.
> 🚫 **Mistake 2:** In Java, primitives are pass-by-value; objects are pass-by-reference (technically pass-by-value of the reference).
> 🚫 **Mistake 3:** Forgetting `RETURN` in a function that should return a value.
> 🚫 **Mistake 4:** Calling a function before defining it (in some languages).

---

## ⚡ One-Minute Recap

- Function: named, reusable code block with parameters and return value
- Recursion: function calls itself, needs base case + recursive case
- Pass by value: copy passed (primitives) | Pass by reference: address passed (objects)
- Recursion uses O(n) stack space | Iteration uses O(1)
- Factorial, Fibonacci, tree traversal = classic recursion examples

---

## 📝 Probable Exam Questions

> **5-mark:** Write a recursive function for Fibonacci. Trace it for n=5.
> **Write:** Write a function to check if a number is palindrome.
> **Explain:** What is the difference between pass by value and pass by reference?
> **Convert:** Convert the recursive factorial function to an iterative version.

---

---

# 6. Coordinate Movement Problems

## 💡 Intuition First

> Coordinate movement problems involve a point (or robot/player) moving on a 2D grid. You track its position (x, y) and update it based on direction commands. These are very common in JUST-style exams.

**Real-world analogy:** A robot on a grid floor — you give it commands (move north, east, south, west) and track where it ends up.

---

## 📐 Basic Coordinate System

```
y
↑
3 │  .  .  .  .
2 │  .  .  .  .
1 │  .  .  .  .
0 │  .  .  .  .
  └──────────────► x
     0  1  2  3

Start: (0, 0)
North (+y): y increases
South (-y): y decreases
East  (+x): x increases
West  (-x): x decreases
```

---

## 📐 Direction Mapping

```
Direction │ Δx │ Δy
──────────┼────┼────
North (N) │  0 │ +1
South (S) │  0 │ -1
East  (E) │ +1 │  0
West  (W) │ -1 │  0

Using arrays for direction:
  dx[] = {0, 0, 1, -1}   // N, S, E, W
  dy[] = {1, -1, 0, 0}   // N, S, E, W
```

---

## ✏️ Worked Example 1: Final Position

```
Problem: A robot starts at (0,0). Given a sequence of moves
         [N, N, E, S, W, N], find the final position.

Algorithm:
START
  SET x ← 0, y ← 0
  FOR each move in moves DO
    IF move = 'N' THEN y ← y + 1
    ELSE IF move = 'S' THEN y ← y - 1
    ELSE IF move = 'E' THEN x ← x + 1
    ELSE IF move = 'W' THEN x ← x - 1
    ENDIF
  ENDFOR
  OUTPUT "Final position: (", x, ",", y, ")"
END

Trace: [N, N, E, S, W, N]
  Start: (0,0)
  N: (0,1)
  N: (0,2)
  E: (1,2)
  S: (1,1)
  W: (0,1)
  N: (0,2)
  Final: (0, 2) ✅
```

---

## ✏️ Worked Example 2: Distance from Origin

```
Problem: After all moves, find the Manhattan distance from origin.

Manhattan distance = |x| + |y|

After moves [N,N,E,S,W,N]: final = (0,2)
Distance = |0| + |2| = 2
```

---

## ✏️ Worked Example 3: Turning Robot

```
Problem: Robot faces North initially. Commands: F (forward), L (turn left), R (turn right).
         Find final position after: F, F, R, F, L, F

Directions (clockwise): N=0, E=1, S=2, W=3
Turn right: dir = (dir + 1) % 4
Turn left:  dir = (dir + 3) % 4  (or (dir - 1 + 4) % 4)

dx[] = {0, 1, 0, -1}   // N, E, S, W
dy[] = {1, 0, -1, 0}   // N, E, S, W

Algorithm:
  x=0, y=0, dir=0 (North)
  F: x+=dx[0]=0, y+=dy[0]=1 → (0,1)
  F: (0,2)
  R: dir=(0+1)%4=1 (East)
  F: x+=dx[1]=1, y+=dy[1]=0 → (1,2)
  L: dir=(1+3)%4=0 (North)
  F: (1,3)
  Final: (1,3) ✅
```

---

## ✏️ Worked Example 4: Grid Boundary Check

```
Problem: Robot on 5×5 grid (0-4, 0-4). Ignore moves that go out of bounds.

FUNCTION isValid(x, y)
  RETURN x >= 0 AND x <= 4 AND y >= 0 AND y <= 4
END FUNCTION

FOR each move DO
  newX ← x + dx[dir]
  newY ← y + dy[dir]
  IF isValid(newX, newY) THEN
    x ← newX
    y ← newY
  ENDIF
ENDFOR
```

---

## 📐 Common Coordinate Patterns

```
8-directional movement (including diagonals):
  dx[] = {-1,-1,-1, 0, 0, 1, 1, 1}
  dy[] = {-1, 0, 1,-1, 1,-1, 0, 1}

Spiral traversal, BFS on grid, flood fill:
  All use coordinate movement with a queue

Distance formulas:
  Manhattan: |x1-x2| + |y1-y2|
  Euclidean: sqrt((x1-x2)² + (y1-y2)²)
  Chebyshev: max(|x1-x2|, |y1-y2|)
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Confusing x (horizontal) and y (vertical) — x is left-right, y is up-down.
> 🚫 **Mistake 2:** Turning: right turn increases direction index, left turn decreases.
> 🚫 **Mistake 3:** Forgetting modulo when wrapping direction: `(dir + 1) % 4`.
> 🚫 **Mistake 4:** Not checking boundary conditions before moving.

---

## ⚡ One-Minute Recap

- N: y+1 | S: y-1 | E: x+1 | W: x-1
- Turning robot: use direction index 0-3, modulo 4
- Manhattan distance: |x| + |y|
- Always check boundary before moving on bounded grid
- Use dx[], dy[] arrays for clean direction handling

---

## 📝 Probable Exam Questions

> **5-mark:** A robot starts at (0,0) facing North. Given commands [F,F,R,F,F,L,F], find final position and direction.
> **Write:** Write pseudocode to find the final position of a robot given a sequence of N/S/E/W moves.
> **Calculate:** After moves [N,N,N,E,E,S,W], what is the Manhattan distance from origin?

---

---

# 7. Pattern & Problem-Solving Algorithms

## 💡 Intuition First

> Pattern problems test your ability to **identify structure and write loops** to produce it. Problem-solving algorithms test your ability to **break down a problem** into logical steps. Both are extremely common in JUST-style exams.

---

## 📐 Star Pattern Problems

### Right Triangle

```
Pattern:
*
**
***
****
*****

Algorithm:
FOR i ← 1 TO n DO
  FOR j ← 1 TO i DO
    OUTPUT "*"
  ENDFOR
  OUTPUT newline
ENDFOR

Trace for n=4:
  i=1: j=1 → *
  i=2: j=1,2 → **
  i=3: j=1,2,3 → ***
  i=4: j=1,2,3,4 → ****
```

### Inverted Triangle

```
Pattern (n=4):
****
***
**
*

FOR i ← n TO 1 STEP -1 DO
  FOR j ← 1 TO i DO
    OUTPUT "*"
  ENDFOR
  OUTPUT newline
ENDFOR
```

### Pyramid

```
Pattern (n=4):
   *
  ***
 *****
*******

FOR i ← 1 TO n DO
  // Print spaces
  FOR j ← 1 TO n-i DO
    OUTPUT " "
  ENDFOR
  // Print stars
  FOR j ← 1 TO 2*i-1 DO
    OUTPUT "*"
  ENDFOR
  OUTPUT newline
ENDFOR

Trace for n=3:
  i=1: 2 spaces, 1 star  →   *
  i=2: 1 space,  3 stars →  ***
  i=3: 0 spaces, 5 stars → *****
```

### Diamond

```
Pattern (n=3):
  *
 ***
*****
 ***
  *

// Upper half (pyramid):
FOR i ← 1 TO n DO
  print (n-i) spaces, (2i-1) stars
ENDFOR
// Lower half (inverted pyramid, skip middle):
FOR i ← n-1 TO 1 STEP -1 DO
  print (n-i) spaces, (2i-1) stars
ENDFOR
```

### Number Patterns

```
Pattern 1:          Pattern 2:
1                   1
1 2                 2 2
1 2 3               3 3 3
1 2 3 4             4 4 4 4

Pattern 1:          Pattern 2:
FOR i←1 TO n DO     FOR i←1 TO n DO
  FOR j←1 TO i DO     FOR j←1 TO i DO
    OUTPUT j             OUTPUT i
  ENDFOR               ENDFOR
  OUTPUT newline       OUTPUT newline
ENDFOR              ENDFOR
```

---

## 📐 Classic Problem-Solving Algorithms

### GCD (Euclidean Algorithm)

```
FUNCTION gcd(a, b)
  WHILE b ≠ 0 DO
    SET temp ← b
    SET b ← a MOD b
    SET a ← temp
  ENDWHILE
  RETURN a
END FUNCTION

Trace: gcd(48, 18)
  a=48, b=18: temp=18, b=48%18=12, a=18
  a=18, b=12: temp=12, b=18%12=6,  a=12
  a=12, b=6:  temp=6,  b=12%6=0,   a=6
  b=0 → return 6 ✅

LCM(a,b) = (a × b) / gcd(a,b)
```

### Check Palindrome

```
FUNCTION isPalindrome(str)
  SET left ← 0
  SET right ← length(str) - 1
  WHILE left < right DO
    IF str[left] ≠ str[right] THEN
      RETURN FALSE
    ENDIF
    SET left ← left + 1
    SET right ← right - 1
  ENDWHILE
  RETURN TRUE
END FUNCTION

Trace: "racecar"
  left=0,right=6: r=r ✅
  left=1,right=5: a=a ✅
  left=2,right=4: c=c ✅
  left=3,right=3: left≥right → exit
  Return TRUE ✅
```

### Count Digits

```
FUNCTION countDigits(n)
  SET count ← 0
  WHILE n > 0 DO
    SET n ← n / 10    (integer division)
    SET count ← count + 1
  ENDWHILE
  RETURN count
END FUNCTION

Trace: n=1234
  n=123, count=1
  n=12,  count=2
  n=1,   count=3
  n=0,   count=4
  Return 4 ✅
```

### Reverse a Number

```
FUNCTION reverseNumber(n)
  SET reversed ← 0
  WHILE n > 0 DO
    SET digit ← n MOD 10
    SET reversed ← reversed * 10 + digit
    SET n ← n / 10
  ENDWHILE
  RETURN reversed
END FUNCTION

Trace: n=1234
  digit=4, reversed=4,   n=123
  digit=3, reversed=43,  n=12
  digit=2, reversed=432, n=1
  digit=1, reversed=4321,n=0
  Return 4321 ✅
```

### Armstrong Number Check

```
A number is Armstrong if sum of cubes of digits = number
Example: 153 = 1³ + 5³ + 3³ = 1 + 125 + 27 = 153 ✅

FUNCTION isArmstrong(n)
  SET original ← n
  SET sum ← 0
  WHILE n > 0 DO
    SET digit ← n MOD 10
    SET sum ← sum + digit³
    SET n ← n / 10
  ENDWHILE
  RETURN sum = original
END FUNCTION
```

### Two Sum Problem

```
Problem: Find two indices in array where arr[i] + arr[j] = target

Brute force O(n²):
FOR i ← 0 TO n-2 DO
  FOR j ← i+1 TO n-1 DO
    IF arr[i] + arr[j] = target THEN
      OUTPUT i, j
      RETURN
    ENDIF
  ENDFOR
ENDFOR

Optimized O(n) using hash map:
SET seen ← empty map
FOR i ← 0 TO n-1 DO
  SET complement ← target - arr[i]
  IF complement IN seen THEN
    OUTPUT seen[complement], i
    RETURN
  ENDIF
  seen[arr[i]] ← i
ENDFOR
```

### FizzBuzz

```
FOR i ← 1 TO n DO
  IF i MOD 15 = 0 THEN
    OUTPUT "FizzBuzz"
  ELSE IF i MOD 3 = 0 THEN
    OUTPUT "Fizz"
  ELSE IF i MOD 5 = 0 THEN
    OUTPUT "Buzz"
  ELSE
    OUTPUT i
  ENDIF
ENDFOR

Key: Check 15 (divisible by both 3 and 5) FIRST
```

---

## 📐 Frequency Count Pattern

```
Problem: Count frequency of each element in array

FUNCTION countFrequency(arr, n)
  SET freq ← empty map
  FOR i ← 0 TO n-1 DO
    IF arr[i] IN freq THEN
      freq[arr[i]] ← freq[arr[i]] + 1
    ELSE
      freq[arr[i]] ← 1
    ENDIF
  ENDFOR
  RETURN freq
END FUNCTION

Trace: arr=[1,2,1,3,2,1]
  freq={1:1}
  freq={1:1, 2:1}
  freq={1:2, 2:1}
  freq={1:2, 2:1, 3:1}
  freq={1:2, 2:2, 3:1}
  freq={1:3, 2:2, 3:1}
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** In pyramid pattern, stars = 2i-1 (not 2i). For i=1: 1 star, i=2: 3 stars.
> 🚫 **Mistake 2:** GCD: always `b = a MOD b`, then `a = old b` — don't swap wrong.
> 🚫 **Mistake 3:** Palindrome: compare from both ends simultaneously, stop when they meet.
> 🚫 **Mistake 4:** FizzBuzz: check divisible by 15 FIRST (before 3 and 5 separately).

---

## ⚡ One-Minute Recap

- Patterns: outer loop = rows, inner loop = columns
- Pyramid: spaces = n-i, stars = 2i-1
- GCD: Euclidean algorithm (a, b) → (b, a%b) until b=0
- Palindrome: two-pointer from both ends
- Reverse number: extract digit (n%10), build reversed (r*10+digit)
- FizzBuzz: check 15 before 3 and 5

---

## 📝 Probable Exam Questions

> **5-mark:** Write pseudocode to print a pyramid pattern of stars for n rows. Trace for n=4.
> **Write:** Write pseudocode to find GCD of two numbers using Euclidean algorithm. Trace for (48, 18).
> **Write:** Write pseudocode to check if a number is a palindrome.
> **Solve:** Write pseudocode for FizzBuzz from 1 to 20.

---

---

# 🏁 Master Quick Revision Sheet — Programming Fundamentals

## ⚡ Pseudocode Keywords Cheat Sheet

```
INPUT / READ          → get user input
OUTPUT / PRINT        → display result
SET / LET             → assign value
IF / THEN / ELSE / ENDIF → conditional
WHILE / DO / ENDWHILE → while loop
FOR / TO / STEP / ENDFOR → for loop
REPEAT / UNTIL        → do-while loop
FUNCTION / RETURN     → define/return from function
CALL                  → invoke function
BREAK / CONTINUE      → loop control
MOD                   → modulo (remainder)
DIV                   → integer division
AND / OR / NOT        → logical operators
```

## 🔑 Key Algorithms Quick Reference

```
GCD(a,b):
  while b≠0: temp=b, b=a%b, a=temp; return a

Palindrome check:
  left=0, right=n-1
  while left<right: if s[left]≠s[right] return false; left++; right--
  return true

Reverse number:
  while n>0: digit=n%10; rev=rev*10+digit; n=n/10

Count digits:
  while n>0: n=n/10; count++

Armstrong check:
  sum of (each digit)³ == original number

Fibonacci (iterative):
  a=0, b=1; for i=2 to n: c=a+b; a=b; b=c; return b

Prime check:
  for i=2 to sqrt(n): if n%i==0 return false; return true
```

## 🧠 Pattern Formulas

```
Right triangle (n rows):
  Row i: i stars

Inverted triangle:
  Row i (from n to 1): i stars

Pyramid (n rows):
  Row i: (n-i) spaces, (2i-1) stars

Diamond (n rows):
  Upper: row i: (n-i) spaces, (2i-1) stars
  Lower: row i (n-1 to 1): (n-i) spaces, (2i-1) stars
```

## 🎯 Top 10 Most Probable Exam Questions

1. Write pseudocode for bubble sort + trace on given array
2. Write pseudocode to find max/min in array
3. Write recursive factorial + trace
4. Write recursive Fibonacci + trace
5. Print pyramid pattern for n rows + trace
6. GCD using Euclidean algorithm + trace
7. Check palindrome (string or number) + trace
8. Coordinate movement: find final position of robot
9. FizzBuzz pseudocode
10. Two-pointer technique: reverse array or palindrome check

## 📊 Loop Selection Guide

```
Know exact count?     → FOR loop
Unknown count?        → WHILE loop
Must run at least once? → DO-WHILE (REPEAT-UNTIL)
Nested patterns?      → Nested FOR loops
```

---

> 📌 **End of Subject 10: Programming Fundamentals**
>
> 🎉 **Tier S (Must Master) Complete!** Subjects 01-06 done.
> Next: **Subject 11 — Discrete Mathematics** (Tier B) →

---

*Handbook generated for MSc Admission Preparation | JUST-Style Exam Focus*
*Version 1.0 | Programming Fundamentals*
