---
type: pattern
area: sde
title: Two Pointer Technique
aliases: [Two Pointer Technique, Two Pointers]
tags: [dsa, arrays, two-pointer, string]
status: draft
source_count: 10
created: 2026-07-12
updated: 2026-07-12
---

## Summary
Two indices walk the array/string in coordination instead of a nested loop, collapsing an O(n²) scan into O(n) (or O(n log n) after a sort). Reach for it when the data is sorted (or you can afford to sort it) and progress depends on comparing the values at two positions. Two flavours dominate:
- **Converging ends** — `left` at the front, `right` at the back, moving toward each other based on a comparison against a target. Ideal on sorted arrays and palindrome checks.
- **Slow / fast** — both start near the front; `fast` scans every element while `slow` marks the write position for a compacted/filtered result. Ideal for in-place removal and partitioning.

## How it works
Converging ends (sorted array, hunt a pair summing to a target):

```cpp
int s = 0, e = size - 1;
while (s < e) {
    int sum = nums[s] + nums[e];
    if (sum == target) return {s, e};
    else if (sum > target) e--;   // too big, shrink from the right
    else s++;                     // too small, grow from the left
}
```

Slow / fast (compact in place, O(1) space): `fast` reads every element, and whenever it finds one worth keeping, `slow` overwrites the next output slot and advances. Everything from `slow` onward is scratch space.

## Problems
- [[Two Sum]] (LC 1) — third approach: sort `(value, index)` pairs, then converge `s`/`e` from both ends until the pair sums to target.
- [[3Sum]] (LC 15) — fix `nums[i]`, then converge two pointers over the remaining suffix to hit `-nums[i]`.
- [[3Sum Closest]] (LC 16) — fix `i`, converge `j`/`k` and track the sum with the smallest `abs(target - sum)`.
- [[4Sum]] (LC 18) — fix two indices, then converge the inner two pointers to the residual target.
- [[Remove Duplicates from Sorted Array]] (LC 26) — slow/fast: `fast` scans, `slow` writes only when `nums[fast] != nums[fast-1]`.
- [[Merge Sorted Array]] (LC 88) — three pointers from the back (`i`, `j`, `k`) merge in place without clobbering unread values.
- [[Valid Palindrome]] (LC 125) — the idiomatic solution converges `l`/`r` inward comparing characters (sidesteps the note's recursive helper).
- [[Move Zeroes]] (LC 283) — slow/fast: `slow` collects non-zeros to the front, then a tail loop fills zeros.
- [[Squares of a Sorted Array]] (LC 977) — converge from both ends picking the larger `abs` and writing squares back-to-front.
- [[The Two Sneaky Numbers of Digitville]] (LC 3289) — after sorting, slow/fast adjacent-pair scan flags duplicates.

## Related
[[k-Sum Pattern]] · [[Sliding Window]] · [[In-place Array Reversal]]

## Sources
- [[Two Sum]] — sorted-pairs converging variant
- [[3Sum]] — fix-one + two-pointer core with dedup
- [[3Sum Closest]] — minimize distance to target
- [[4Sum]] — two fixed + two converging
- [[Remove Duplicates from Sorted Array]] — canonical slow/fast compaction
- [[Merge Sorted Array]] — back-to-front three-pointer merge
- [[Valid Palindrome]] — converging character comparison
- [[Move Zeroes]] — slow/fast partition then zero-fill
- [[Squares of a Sorted Array]] — converge on largest magnitude
- [[The Two Sneaky Numbers of Digitville]] — sorted adjacent-duplicate scan
