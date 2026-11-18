---
type: source
area: sde
title: 1492 The kth Factor of n
aliases: [1492 The kth Factor of n, The kth Factor of n]
tags: [dsa, math, number-theory]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/1492 The kth Factor of n 250e9c4cbab8807c8cf0de570e2817ca.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Return the `k`-th smallest factor of `n`, or `-1` if fewer than `k` exist. The scalable idea uses the fact that factors pair up around √n: enumerate divisors below √n ascending, then divisors from √n down (via `n/i`), counting down `k` and handling the perfect-square case so the root isn't double-counted.

## Approaches
- **Collect all factors** — loop `i` from 1 to `n`, push every divisor into a vector, return index `k-1` (or `-1`). O(n) time, O(n) space.
- **Count down to the k-th** — loop 1..n, decrement `k` on each divisor, return `i` when `k` hits 0. O(min(n, k)) time (stops early), O(1) space.
- **Square-root split** — first loop `i` from 1 while `i < √n`, counting small divisors; second loop `i` from ⌊√n⌋ down to 1, counting the large divisors as `n/i`. Excluding `i == √n` from the first loop and starting the second at ⌊√n⌋ counts a perfect-square root exactly once. O(√n) time, O(1) space.

## Best solution
```cpp
class Solution {
public:
    int kthFactor(int n, int k) {
        for (int i = 1; i < sqrt(n); ++i) {
            if (n % i == 0) k--;
            if (k == 0) return i;
        }
        for (int i = (int) sqrt(n); i >= 1; --i) {
            if (n % (n / i) == 0) k--;
            if (k == 0) return n / i;
        }
        return -1;
    }
};
```
Optimal because divisors are symmetric about √n, so scanning only up to √n (twice) finds all of them in O(√n) rather than O(n).

## Notes
- Edge case — perfect squares (n = 9, 16, …): the first loop uses `i < √n` (strict) so it skips the root, and the second loop starts at ⌊√n⌋ so the root is counted once there. This avoids both missing and double-counting it.
- The second loop checks `n % (n/i) == 0`, which is logically identical to `n % i == 0`; the note keeps it in the `n/i` form purely for readability.
- The count-down (O(min(n,k))) version is the simplest to remember when `k` is small.

## Sources
- [[1492 The kth Factor of n]] raw note — `raw/notes/DSA/DSA/1492 The kth Factor of n 250e9c4cbab8807c8cf0de570e2817ca.md`
