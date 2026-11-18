---
type: source
area: sde
title: 724 Find Pivot Index
aliases: [724 Find Pivot Index, Find Pivot Index]
tags: [dsa, arrays, prefix-sum]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/724 Find Pivot Index 2761173c00ff435884886e817ca4835f.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Find the leftmost index where the sum of everything to its left equals the sum of everything to its right. The optimal one-pass approach computes the total sum once, then derives the right sum by subtraction as it walks left to right, needing no second array.

## Approaches
- **Brute force** — at each index, `accumulate` the left and right slices separately. O(n^2) time, O(1) space.
- **Two prefix-sum arrays** — precompute left-to-right and right-to-left prefix sums, then find the index where they match. O(n) time, O(n) space.
- **Single-pass running left sum (optimal)** — compute the total `sum`; walking left to right, subtract `nums[i]` from `sum` to get the right sum, compare against the running `left` sum, then add `nums[i]` into `left`. O(n) time, O(1) space.

## Best solution
```cpp
class Solution {
public:
    int pivotIndex(vector<int>& nums) {
        int left = 0, sum = 0;
        for (int i = 0; i < nums.size(); ++i) sum += nums[i];

        for (int i = 0; i < nums.size(); ++i) {
            sum -= nums[i];             // sum now holds the right-side total
            if (sum == left) return i;  // left == right => pivot
            left += nums[i];
        }
        return -1;
    }
};
```
Optimal: O(1) space because the right sum is derived by subtraction from the total rather than stored in a second prefix array.

## Notes
- The note recorded "I still don't understand how it works out" for this one-pass trick.

> [!note] Claude's addition
> **Why the O(1) trick works.** Compute the total sum `S` once. Walk left→right keeping `leftSum`, the sum of everything strictly before `i`. At index `i`, the right sum is whatever remains after removing the left part and `nums[i]` itself: `S - leftSum - nums[i]`. So `i` is a pivot exactly when `leftSum == S - leftSum - nums[i]`. Then update `leftSum += nums[i]` before moving on. It is O(1) space because you DERIVE the right sum by subtraction instead of precomputing a second prefix array — one pass, no extra storage. (The code above folds this into a single mutated `sum` variable, subtracting `nums[i]` first so `sum` becomes the right total.)

## Techniques
[[Prefix Sum]]

## Sources
- [[724 Find Pivot Index]] raw note — see `raw_path` above.
