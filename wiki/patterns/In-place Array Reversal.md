---
type: pattern
area: sde
title: In-place Array Reversal
aliases: [In-place Array Reversal, Reversal Trick]
tags: [dsa, arrays, in-place]
status: draft
source_count: 3
created: 2026-07-12
updated: 2026-07-12
---

## Summary
Reversing a segment (or the whole array) in place is a cheap O(1)-space primitive that composes into surprisingly powerful rearrangements. The headline trick: **rotating an array by `k` = reverse all, then reverse the first `k`, then reverse the rest**. More generally, a final "reverse the suffix" step is how you turn a just-mutated array into its lexicographically smallest tail (next-permutation) or how you flip a transposed matrix row into a rotation.

## How it works
Rotate-by-reversal (three reversals, O(1) space):

```cpp
k = k % size;                              // drop useless full rotations
reverse(nums.begin(), nums.end());         // whole array
reverse(nums.begin(), nums.begin() + k);   // first k
reverse(nums.begin() + k, nums.end());     // remaining
```

Reversing the whole array puts the last `k` elements at the front but in wrong order; the two partial reversals fix each block's internal order. The same "reverse the tail" idea appears in next-permutation: after swapping the dip element with its next-greater successor, the suffix is descending, so `reverse` makes it ascending = the smallest continuation. In matrix rotation, transpose then reverse each row.

## Problems
- [[Next Permutation]] (LC 31) — find the descending-from-right dip, swap with its next-greater, then reverse the suffix to minimize it.
- [[Rotate Image]] (LC 48) — transpose across the diagonal, then reverse each row to rotate 90 degrees in place.
- [[Rotate Array]] (LC 189) — the three-reversal rotate-by-k trick, O(1) space.

## Related
[[Matrix Traversal]] · [[Two Pointer Technique]]

## Sources
- [[Next Permutation]] — reverse-the-suffix to get the smallest tail
- [[Rotate Image]] — transpose + row-reverse rotation
- [[Rotate Array]] — three-reversal rotation
