---
type: pattern
area: sde
title: Prefix Sum
aliases: [Prefix Sum, Cumulative Sum]
tags: [dsa, arrays, prefix-sum]
status: draft
source_count: 5
created: 2026-07-12
updated: 2026-07-12
---

## Summary
Precompute cumulative aggregates so any range query becomes an O(1) subtraction. The prefix sum `P[i]` = sum of `nums[0..i]`; then the sum of any subarray `[l, r]` is `P[r] - P[l-1]`. Reach for it whenever you repeatedly need range sums, "sum before / after this index", or subarray-sum counts. Common variants: two-directional prefixes (prefix + suffix), a running-sum in place, a prefix over a tally/frequency array, and prefix-sum paired with a hashmap for subarray counting.

## How it works
Base case — build a running sum in place:

```cpp
for (int i = 1; i < size; ++i) nums[i] += nums[i-1];   // nums[i] now = prefix sum up to i
```

Two-directional (prefix × suffix) avoids division in [[Product of Array Except Itself]]: one left pass fills each slot with the product of everything before it, one right pass multiplies in everything after — the element itself is never included.

The single-pass pivot trick derives the right sum by subtraction instead of storing a second array (O(1) space): keep a total `S` and a running `leftSum`; at index `i` the right sum is `S - leftSum - nums[i]`.

Paired with a hashmap it counts subarrays: seed `mp[0] = 1`, and at each running `prefixSum` add `mp[prefixSum - k]` (how many earlier prefixes make a `[..]` window summing to `k`) — see [[Subarray Sum Equals K]].

## Problems
- [[Product of Array Except Itself]] (LC 238) — prefix-product left pass then suffix-product right pass, no division, O(1) extra space.
- [[Subarray Sum Equals K]] (LC 560) — running prefix sum + hashmap of prefix frequencies; count `mp[prefixSum - k]` (seed `mp[0]=1`).
- [[Find Pivot Index]] (LC 724) — total sum minus running left sum yields the right sum in one O(1)-space pass.
- [[How Many Numbers Are Smaller Than the Current Number]] (LC 1365) — tally counts into a size-101 array, prefix-sum it, so `tally[v-1]` = how many values are smaller than `v`.
- [[Running Sum of 1d Array]] (LC 1480) — the definition itself: overwrite each element with the cumulative sum up to it.

## Related
[[Hashmap Lookup Pattern]] · [[Sliding Window]]

## Sources
- [[Product of Array Except Itself]] — bidirectional prefix/suffix products
- [[Subarray Sum Equals K]] — prefix sum + hashmap subarray counting
- [[Find Pivot Index]] — O(1)-space right-sum-by-subtraction
- [[How Many Numbers Are Smaller Than the Current Number]] — prefix sum over a tally array
- [[Running Sum of 1d Array]] — the canonical in-place running sum
