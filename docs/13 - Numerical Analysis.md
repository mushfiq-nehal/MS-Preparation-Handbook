# 📘 MSc Admission Prep — Subject 13: Numerical Analysis
### 🎯 JUST-Style Exam Handbook | Tier B — Moderately Important

---

## 📋 Table of Contents

| # | Topic |
|---|-------|
| 1 | [Bisection Method](#1-bisection-method) |
| 2 | [Newton-Raphson Method](#2-newton-raphson-method) |
| 3 | [Interpolation](#3-interpolation) |
| 4 | [Numerical Integration](#4-numerical-integration) |
| 5 | [Error Analysis](#5-error-analysis) |

---

# 1. Bisection Method

## 💡 Intuition First

> The bisection method finds a root of f(x)=0 by **repeatedly halving an interval** that contains the root. Like a number guessing game — "Is it higher or lower than 50? Higher. Is it higher or lower than 75? Lower..." — you narrow down to the answer.

**Requirement:** f(a) and f(b) must have opposite signs (f(a)×f(b) < 0) — guarantees a root exists between a and b (Intermediate Value Theorem).

---

## 📐 Algorithm

```
FUNCTION bisection(f, a, b, tolerance)
  IF f(a) × f(b) > 0 THEN
    ERROR "No root in [a,b]"
  ENDIF

  WHILE (b - a) / 2 > tolerance DO
    c ← (a + b) / 2      ← midpoint
    IF f(c) = 0 THEN
      RETURN c            ← exact root found
    ENDIF
    IF f(a) × f(c) < 0 THEN
      b ← c               ← root in [a, c]
    ELSE
      a ← c               ← root in [c, b]
    ENDIF
  ENDWHILE
  RETURN (a + b) / 2
END FUNCTION
```

---

## ✏️ Worked Example

```
Find root of f(x) = x³ - x - 2 in [1, 2]

f(1) = 1 - 1 - 2 = -2  (negative)
f(2) = 8 - 2 - 2 = 4   (positive)
f(1) × f(2) < 0 → root exists ✅

Iteration 1:
  c = (1+2)/2 = 1.5
  f(1.5) = 3.375 - 1.5 - 2 = -0.125 (negative)
  f(1) × f(1.5) < 0 → root in [1, 1.5]? No!
  f(1.5) × f(2) < 0 → root in [1.5, 2]
  a = 1.5, b = 2

Iteration 2:
  c = (1.5+2)/2 = 1.75
  f(1.75) = 5.359 - 1.75 - 2 = 1.609 (positive)
  f(1.5) × f(1.75) < 0 → root in [1.5, 1.75]
  b = 1.75

Iteration 3:
  c = (1.5+1.75)/2 = 1.625
  f(1.625) = 4.291 - 1.625 - 2 = 0.666 (positive)
  root in [1.5, 1.625]
  b = 1.625

Converging to root ≈ 1.5214...

Number of iterations needed for accuracy ε:
  n ≥ log₂((b-a)/ε)
  For ε=0.001, [1,2]: n ≥ log₂(1000) ≈ 10 iterations
```

---

## ⚖️ Bisection Properties

| Property | Value |
|----------|-------|
| Convergence | Always (if root exists in interval) |
| Rate | Linear (slow) |
| Iterations for ε | log₂((b-a)/ε) |
| Requirement | f(a)×f(b) < 0 |
| Simplicity | Very simple |

---

## ⚡ One-Minute Recap

- Bisection: halve interval containing root repeatedly
- Requirement: f(a)×f(b) < 0 (opposite signs)
- Always converges but slowly (linear convergence)
- Iterations needed: log₂((b-a)/ε)

---

## 📝 Probable Exam Questions

> **5-mark:** Apply bisection method to find root of f(x)=x²-3 in [1,2]. Show 3 iterations.
> **Short note:** What is the convergence rate of the bisection method?

---

---

# 2. Newton-Raphson Method

## 💡 Intuition First

> Newton-Raphson uses the **tangent line** at a point to find a better approximation of the root. Like sliding down a slope toward the bottom — each step gets you closer, and it converges much faster than bisection.

**Geometric idea:** Draw a tangent to f(x) at current guess xₙ. Where the tangent crosses the x-axis is the next guess xₙ₊₁.

---

## 📐 Formula

```
xₙ₊₁ = xₙ - f(xₙ) / f'(xₙ)

where f'(xₙ) is the derivative of f at xₙ

Derivation:
  Tangent line at (xₙ, f(xₙ)):
    y - f(xₙ) = f'(xₙ)(x - xₙ)
  Set y = 0 (x-intercept):
    -f(xₙ) = f'(xₙ)(x - xₙ)
    x = xₙ - f(xₙ)/f'(xₙ)
```

---

## ✏️ Worked Example

```
Find root of f(x) = x³ - x - 2
f'(x) = 3x² - 1

Starting guess: x₀ = 1.5

Iteration 1:
  f(1.5)  = 3.375 - 1.5 - 2 = -0.125
  f'(1.5) = 3(2.25) - 1 = 5.75
  x₁ = 1.5 - (-0.125)/5.75 = 1.5 + 0.0217 = 1.5217

Iteration 2:
  f(1.5217)  = 3.528 - 1.5217 - 2 = 0.006
  f'(1.5217) = 3(2.316) - 1 = 5.948
  x₂ = 1.5217 - 0.006/5.948 = 1.5217 - 0.001 = 1.5214

Iteration 3:
  f(1.5214) ≈ 0.000003 (very close to 0!)
  x₃ ≈ 1.5214

Root ≈ 1.5214 (converged in 3 iterations vs 10+ for bisection!)
```

---

## ⚖️ Newton-Raphson Properties

| Property | Value |
|----------|-------|
| Convergence | Quadratic (very fast) |
| Requirement | f'(x) ≠ 0 at root, good initial guess |
| Failure | f'(xₙ) = 0 (division by zero) |
| Failure | Poor initial guess → diverge |
| Simplicity | Requires derivative |

---

## ⚖️ Bisection vs Newton-Raphson

| Feature | Bisection | Newton-Raphson |
|---------|-----------|----------------|
| Convergence | Linear (slow) | Quadratic (fast) |
| Guarantee | Always converges | May diverge |
| Requirement | f(a)×f(b)<0 | f'(x) needed |
| Iterations | Many | Few |
| Simplicity | Simple | Needs derivative |

---

## ⚡ One-Minute Recap

- Newton-Raphson: xₙ₊₁ = xₙ - f(xₙ)/f'(xₙ)
- Uses tangent line to find next approximation
- Quadratic convergence — much faster than bisection
- Fails if f'(xₙ)=0 or initial guess is poor

---

## 📝 Probable Exam Questions

> **5-mark:** Apply Newton-Raphson to find root of f(x)=x²-2 starting from x₀=1. Show 3 iterations.
> **Compare:** Bisection method vs Newton-Raphson method.

---

# 3. Interpolation

## 💡 Intuition First

> **Interpolation** estimates unknown values between known data points. Like estimating the temperature at 2:30 PM when you only measured at 2:00 PM and 3:00 PM.

---

## 📐 Linear Interpolation

```
Given two points (x₀, y₀) and (x₁, y₁):

y = y₀ + (x - x₀) × (y₁ - y₀) / (x₁ - x₀)

Example: Find f(2.5) given f(2)=4, f(3)=9
  y = 4 + (2.5-2) × (9-4)/(3-2)
    = 4 + 0.5 × 5
    = 4 + 2.5 = 6.5
```

---

## 📐 Lagrange Interpolation

```
Given n+1 points (x₀,y₀), (x₁,y₁), ..., (xₙ,yₙ):

P(x) = Σᵢ yᵢ × Lᵢ(x)

where Lᵢ(x) = Π_{j≠i} (x - xⱼ) / (xᵢ - xⱼ)

Example: Find P(2) given (1,1), (3,9), (4,16)

L₀(x) = (x-3)(x-4) / (1-3)(1-4) = (x-3)(x-4) / 6
L₁(x) = (x-1)(x-4) / (3-1)(3-4) = (x-1)(x-4) / (-2)
L₂(x) = (x-1)(x-3) / (4-1)(4-3) = (x-1)(x-3) / 3

P(2) = 1×L₀(2) + 9×L₁(2) + 16×L₂(2)
     = 1×((-1)(-2)/6) + 9×((1)(-2)/(-2)) + 16×((1)(-1)/3)
     = 1×(2/6) + 9×(1) + 16×(-1/3)
     = 0.333 + 9 - 5.333
     = 4

P(2) = 4 ✅ (matches x²: 2²=4)
```

---

## 📐 Newton's Divided Difference

```
More efficient for adding new data points.

Divided differences:
  f[x₀] = f(x₀)
  f[x₀,x₁] = (f[x₁] - f[x₀]) / (x₁ - x₀)
  f[x₀,x₁,x₂] = (f[x₁,x₂] - f[x₀,x₁]) / (x₂ - x₀)

P(x) = f[x₀] + f[x₀,x₁](x-x₀) + f[x₀,x₁,x₂](x-x₀)(x-x₁) + ...
```

---

## ⚡ One-Minute Recap

- Interpolation: estimate values between known data points
- Linear: straight line between two points
- Lagrange: polynomial through all given points
- Newton's divided difference: efficient for adding new points

---

## 📝 Probable Exam Questions

> **5-mark:** Apply Lagrange interpolation to find f(2) given (1,1), (3,27), (4,64).
> **Short note:** What is interpolation? When is it used?

---

---

# 4. Numerical Integration

## 💡 Intuition First

> Numerical integration approximates the area under a curve when we can't compute the integral analytically. Like estimating the area of an irregular field by dividing it into rectangles or trapezoids.

---

## 📐 Trapezoidal Rule

```
Approximate area under f(x) from a to b using trapezoids.

Single trapezoid:
  ∫ₐᵇ f(x)dx ≈ (b-a)/2 × [f(a) + f(b)]

Composite trapezoidal rule (n subintervals, h=(b-a)/n):
  ∫ₐᵇ f(x)dx ≈ h/2 × [f(x₀) + 2f(x₁) + 2f(x₂) + ... + 2f(xₙ₋₁) + f(xₙ)]

Example: ∫₀² x² dx with n=4 (h=0.5)
  x₀=0, x₁=0.5, x₂=1, x₃=1.5, x₄=2
  f(0)=0, f(0.5)=0.25, f(1)=1, f(1.5)=2.25, f(2)=4

  ≈ 0.5/2 × [0 + 2(0.25) + 2(1) + 2(2.25) + 4]
  = 0.25 × [0 + 0.5 + 2 + 4.5 + 4]
  = 0.25 × 11 = 2.75

  Exact: ∫₀² x² dx = [x³/3]₀² = 8/3 ≈ 2.667
  Error = 2.75 - 2.667 = 0.083
```

---

## 📐 Simpson's Rule

```
Uses parabolas instead of trapezoids — more accurate.
Requires EVEN number of subintervals.

Simpson's 1/3 Rule (n even, h=(b-a)/n):
  ∫ₐᵇ f(x)dx ≈ h/3 × [f(x₀) + 4f(x₁) + 2f(x₂) + 4f(x₃) + ... + 4f(xₙ₋₁) + f(xₙ)]

Pattern of coefficients: 1, 4, 2, 4, 2, ..., 4, 1

Example: ∫₀² x² dx with n=4 (h=0.5)
  ≈ 0.5/3 × [f(0) + 4f(0.5) + 2f(1) + 4f(1.5) + f(2)]
  = 0.5/3 × [0 + 4(0.25) + 2(1) + 4(2.25) + 4]
  = 0.5/3 × [0 + 1 + 2 + 9 + 4]
  = 0.5/3 × 16 = 8/3 ≈ 2.667

  Exact answer! Simpson's rule is exact for polynomials up to degree 3.
```

---

## ⚖️ Trapezoidal vs Simpson's

| Feature | Trapezoidal | Simpson's |
|---------|-------------|-----------|
| Shape used | Trapezoid | Parabola |
| Accuracy | O(h²) | O(h⁴) |
| Requirement | Any n | Even n |
| Coefficients | 1,2,2,...,2,1 | 1,4,2,4,...,4,1 |

---

## ⚡ One-Minute Recap

- Trapezoidal: h/2 × [f₀ + 2f₁ + 2f₂ + ... + 2fₙ₋₁ + fₙ]
- Simpson's: h/3 × [f₀ + 4f₁ + 2f₂ + 4f₃ + ... + 4fₙ₋₁ + fₙ]
- Simpson's is more accurate (O(h⁴) vs O(h²))
- Simpson's requires even number of subintervals

---

## 📝 Probable Exam Questions

> **5-mark:** Apply the trapezoidal rule to evaluate ∫₁³ (1/x)dx with n=4. Compare with exact value.
> **5-mark:** Apply Simpson's 1/3 rule to evaluate ∫₀¹ eˣ dx with n=4.

---

# 5. Error Analysis

## 💡 Intuition First

> Numerical methods introduce errors because we use approximations. Understanding error types helps you know how accurate your answer is and how to improve it.

---

## 📐 Types of Errors

```
1. Absolute Error:
   |True value - Approximate value|
   Example: True=3.14159, Approx=3.14 → Error=0.00159

2. Relative Error:
   |True - Approx| / |True|
   Example: 0.00159 / 3.14159 ≈ 0.000506 = 0.05%

3. Percentage Error:
   Relative Error × 100%

4. Round-off Error:
   Due to finite precision of computer arithmetic
   Example: 1/3 = 0.333... stored as 0.3333333

5. Truncation Error:
   Due to approximating infinite processes with finite ones
   Example: Taylor series truncated after n terms
   sin(x) ≈ x - x³/6 + x⁵/120 (truncated)

6. Propagation Error:
   Errors in input data propagate through calculations
```

---

## 📐 Significant Figures

```
Rules for significant figures:
  Non-zero digits: always significant
  Zeros between non-zeros: significant
  Leading zeros: NOT significant
  Trailing zeros after decimal: significant

Examples:
  3.14159  → 6 significant figures
  0.00314  → 3 significant figures (leading zeros don't count)
  3.1400   → 5 significant figures (trailing zeros after decimal count)
  3100     → ambiguous (2, 3, or 4 sig figs — use scientific notation)
  3.1×10³  → 2 significant figures
```

---

## 📐 Convergence Criteria

```
Stop iterative methods when:
  |xₙ₊₁ - xₙ| < ε           (absolute tolerance)
  |xₙ₊₁ - xₙ| / |xₙ₊₁| < ε  (relative tolerance)
  |f(xₙ)| < ε                (function value tolerance)
```

---

## ⚡ One-Minute Recap

- Absolute error: |true - approx|
- Relative error: |true - approx| / |true|
- Round-off: finite precision | Truncation: finite approximation
- Bisection error after n steps: (b-a)/2ⁿ
- Newton-Raphson: quadratic convergence (error squares each step)

---

## 📝 Probable Exam Questions

> **Short note:** What is the difference between round-off error and truncation error?
> **Calculate:** Find absolute and relative error if true value = π and approximation = 3.14.

---

# 🏁 Quick Revision — Numerical Analysis

## Key Formulas

```
Bisection:
  c = (a+b)/2; update a or b based on sign of f(c)
  Iterations needed: n ≥ log₂((b-a)/ε)

Newton-Raphson:
  xₙ₊₁ = xₙ - f(xₙ)/f'(xₙ)
  Quadratic convergence

Trapezoidal Rule:
  h/2 × [f₀ + 2f₁ + 2f₂ + ... + 2fₙ₋₁ + fₙ]

Simpson's 1/3 Rule:
  h/3 × [f₀ + 4f₁ + 2f₂ + 4f₃ + ... + 4fₙ₋₁ + fₙ]

Lagrange Interpolation:
  P(x) = Σᵢ yᵢ × Π_{j≠i} (x-xⱼ)/(xᵢ-xⱼ)
```

## Method Comparison

```
Root Finding:
  Bisection:       Always converges, slow (linear)
  Newton-Raphson:  Fast (quadratic), may diverge

Integration:
  Trapezoidal:     O(h²) error, simple
  Simpson's:       O(h⁴) error, more accurate, needs even n
```

---

> 📌 **End of Subject 13: Numerical Analysis**
>
> 🎉 **All Tier B subjects complete!**
> Tier S (01-06) ✅ | Tier A (07-10) ✅ | Tier B (11-13) ✅

---

*Handbook generated for MSc Admission Preparation | JUST-Style Exam Focus*
*Version 1.0 | Numerical Analysis*
