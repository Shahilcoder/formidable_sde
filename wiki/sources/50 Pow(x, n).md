---
type: source
area: sde
title: 50 Pow(x, n)
aliases: ["50 Pow(x, n)", "Pow(x, n)"]
tags: [dsa, recursion, binary-exponentiation]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/50 Pow(x, n) 1b6e9c4cbab8800cb407f80d2090872c.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Compute `x^n` in O(log n). Binary exponentiation (quick power): square the result of the half-power rather than multiplying `x` by itself `n` times — `a^n = (a^(n/2))^2`, with an extra factor of `a` when `n` is odd. Negative exponents return the reciprocal.

## Approaches
- **Recursive binary exponentiation** — recurse on `qPow(base, exponent/2)`, then square it and multiply by `base` once more if the exponent is odd. Time O(log n), space O(log n) (recursion stack).
- **Iterative binary exponentiation** — walk the bits of the exponent: multiply `result` by the running `base` whenever the low bit is set, square `base` each step, right-shift the exponent. Time O(log n), space O(1).

## Best solution
```cpp
class Solution {
public:
    double qPow(double base, unsigned int exponent) {
        // anything to the power 0 is 1
        if (exponent == 0) return 1.0;

        // head recursion; exponent/2 works for odd or even
        double temp = qPow(base, exponent / 2);

        // if exponent is odd, multiply the extra base
        if (exponent & 1) return base * temp * temp;

        return temp * temp;
    }

    double myPow(double x, int n) {
        // quick power / binary exponentiation
        return n >= 0 ? qPow(x, n) : 1 / qPow(x, -(unsigned int)n);
    }
};
```
Optimal because halving the exponent each call reduces the multiplication count from O(n) to O(log n). The iterative form (in the raw note) trades the stack for O(1) space.

## Notes
- Squaring `temp` once and reusing it (rather than calling `qPow` twice) is what keeps it O(log n) — two recursive calls would blow up to O(n).
- The bitwise `exponent & 1` odd-check and `exponent >>= 1` halving (iterative version) map directly onto the binary digits of the exponent.

> [!note] Claude's addition
> Overflow guard for negative exponents: computing `-n` overflows when `n == INT_MIN`, because the magnitude of `INT_MIN` exceeds `INT_MAX`. The note sidesteps this by casting to `unsigned int` before negating (`-(unsigned int)n`), which safely holds the magnitude; casting to a wider signed type such as `long long` before negating works too. Then return `1 / qPow(x, -n)`.

## Techniques
[[Binary Exponentiation]]

## Sources
- [[50 Pow(x, n)]] raw note — `raw/notes/DSA/DSA/50 Pow(x, n) 1b6e9c4cbab8800cb407f80d2090872c.md`
