---
type: concept
area: sde
title: Binary Exponentiation
aliases: [Binary Exponentiation, Fast Power, Exponentiation by Squaring, Quick Power]
tags: [dsa, recursion, math, divide-and-conquer]
status: draft
source_count: 1
created: 2026-07-12
updated: 2026-07-12
---

## Summary
Binary Exponentiation (a.k.a. fast power / exponentiation by squaring) computes `aⁿ` in **O(log n)** multiplications instead of the naive O(n), by repeatedly squaring the base and halving the exponent. Reach for it whenever an exponent is large — floating-point powers, modular exponentiation, matrix power for linear recurrences.

## How it works
Divide and conquer on the exponent:
- If `n` is even: `aⁿ = (a^(n/2))²`
- If `n` is odd: `aⁿ = a · (a^(n/2))²` (integer division drops the trailing 1, restored by the extra factor of `a`)

Each level halves `n`, so there are O(log n) levels.

Recursive form (LC 50):
```cpp
double qPow(double base, unsigned int exp) {
    if (exp == 0) return 1.0;
    double half = qPow(base, exp / 2);
    if (exp & 1) return base * half * half;   // odd exponent
    return half * half;                        // even exponent
}
double myPow(double x, int n) {
    return n >= 0 ? qPow(x, n) : 1 / qPow(x, -(unsigned int)n);
}
```

An iterative form walks the exponent's bits: multiply the result by the current base power whenever the low bit is set (`exp & 1`), then square the base and right-shift the exponent (`exp >>= 1`).

**INT_MIN overflow guard.** For negative `n` you'd like to compute `1 / pow(x, -n)`, but `-n` **overflows when `n == INT_MIN`**: the magnitude of `INT_MIN` is one larger than `INT_MAX`, so negating it in `int` is undefined/wraps. Fix it by casting to a wider or unsigned type *before* negating — e.g. `-(unsigned int)n` or `1 / qPow(x, -(long long)n)` — so the magnitude is representable.

## Problems
- [[Pow(x, n)]] (LC 50) — halve the exponent and square the base for O(log n); handle negative exponents via reciprocal, casting to unsigned/long long before negating to dodge the `INT_MIN` overflow.

## Related
[[Backtracking]] · [[Bit Packing]]

## Sources
- [[Pow(x, n)]] — recursive and iterative fast-power implementations plus the negative-exponent overflow handling.
