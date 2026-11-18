---
type: pattern
area: sde
title: k-Sum Pattern
aliases: [k-Sum Pattern, kSum]
tags: [dsa, arrays, two-pointer]
status: draft
source_count: 4
created: 2026-07-12
updated: 2026-07-12
---

## Summary
A recursive/iterative recipe for "find `k` numbers that sum to a target": **sort the array once, fix `k-2` outer indices with nested loops, then solve the innermost 2-Sum with a converging [[Two Pointer Technique]]**. Sorting is what makes both the two-pointer step and de-duplication possible. The user's solved set walks the whole ladder: Two Sum → 3Sum → 3Sum Closest → 4Sum, each adding one more fixed layer on top of the same core.

## How it works
The invariant across the family:
1. `sort(nums)`.
2. Fix outer indices with `for` loops; after each, skip duplicate values so identical triplets/quadruplets aren't emitted twice.
3. On the innermost two elements run `left`/`right` converging on the residual target: too small → `left++`, too big → `right--`, match → record and skip duplicates on both sides.

The 3Sum core (2-Sum on a suffix, with dedup):

```cpp
for (int i = 0; i < size - 2; ++i) {
    int left = i + 1, right = size - 1;
    while (left < right) {
        int sum = nums[i] + nums[left] + nums[right];
        if (sum == 0) {
            res.push_back({nums[i], nums[left], nums[right]});
            while (left < right && nums[left]  == nums[left + 1])  left++;
            while (right > left && nums[right] == nums[right - 1]) right--;
            left++; right--;
        } else if (sum > 0) right--;
        else left++;
    }
    while (i < size - 2 && nums[i] == nums[i + 1]) i++;   // dedup the fixed index
}
```

Each extra `k` adds one enclosing loop (and its own dedup skip): 4Sum wraps a second `for (j)` around this block. Complexity is O(n^(k-1)) — O(n²) for 3Sum, O(n³) for 4Sum. Watch for overflow: 4Sum casts the running sum to `long` before comparing.

## Problems
- [[Two Sum]] (LC 1) — the k=2 base case: sorted-pairs + converging two pointers (also solvable with a hashmap).
- [[3Sum]] (LC 15) — k=3: fix one index, 2-Sum the rest to `-nums[i]`, dedup both layers.
- [[3Sum Closest]] (LC 16) — 3Sum variant that minimizes `abs(target - sum)` instead of requiring an exact hit; returns early on an exact match.
- [[4Sum]] (LC 18) — k=4: two fixed loops around the two-pointer core, `long` cast to avoid overflow.

## Related
[[Two Pointer Technique]] · [[Hashmap Lookup Pattern]]

## Sources
- [[Two Sum]] — the 2-Sum base case of the ladder
- [[3Sum]] — fix-one + two-pointer + two-layer dedup
- [[3Sum Closest]] — closest-sum variant of the core
- [[4Sum]] — generalizes to two fixed loops, with overflow guard
