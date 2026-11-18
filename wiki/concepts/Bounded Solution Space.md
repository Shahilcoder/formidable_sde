---
type: concept
area: sde
title: Bounded Solution Space
aliases: [Bounded Solution Space, Constant Solution Space]
tags: [dsa, enumeration, complexity]
status: stub
source_count: 1
created: 2026-07-14
updated: 2026-07-14
---

## Summary
When the set of *possible answers* is provably fixed — bounded by a constant, not by the input size — you can enumerate that entire universe and filter it, and the whole thing is **O(1)**. The trap is measuring complexity against the input's magnitude (a range `[low, high]` up to 10⁹) when the answer space is actually tiny and constant. Recognize the bound first; the "brute force" is then the optimal solution.

## How it works
1. **Prove the universe is constant.** Count the candidates independent of the input. In [[1291 Sequential Digits]] there are exactly 36 sequential-digit numbers (8 of length 2, 7 of length 3, …, 1 of length 9) — no matter how wide `[low, high]` is.
2. **Enumerate all candidates** with constant work (a fixed loop, a lookup table, or slicing a fixed string).
3. **Filter to the query** (in range / matching predicate).
4. **Report O(1)** — the loop bound and any auxiliary storage are constants, not functions of `n`.

The key mental move: complexity is measured against the size of what you *iterate*, and here that's the constant catalog, not the (possibly huge) input range.

## When it applies
- The answer must come from a small, structurally-constrained family (fixed digit patterns, permutations of a tiny alphabet, board states of a fixed-size grid, the 12 months, the 9 sequential-digit lengths).
- You'd otherwise be tempted to scan a large input range checking each element — but the *valid* elements are few and generatable directly.
- Contrast with a genuinely input-sized search space, where enumeration is exponential/linear in `n` and this trick does **not** apply.

## Related
[[Sliding Window]] · [[Backtracking]]

## Sources
- [[1291 Sequential Digits]] — 36 total sequential-digit numbers → enumerate the catalog, filter to `[low, high]`, O(1).
