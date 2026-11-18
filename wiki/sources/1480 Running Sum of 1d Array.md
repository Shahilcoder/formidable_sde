---
type: source
area: sde
title: 1480 Running Sum of 1d Array
aliases: [1480 Running Sum of 1d Array, Running Sum of 1d Array]
tags: [dsa, arrays, prefix-sum]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/1480 Running Sum of 1d Array 751545adcc6d45358ed6b3c90ce1bdd8.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Return the running (cumulative) sum of an array. This is the definition of a prefix sum: each element becomes itself plus everything before it. Done in place by adding the previous (already-accumulated) element to the current one.

## Approaches
- **Accumulator variable** — keep a running total; at each `i`, add the accumulator to `nums[i]` and then add the original `nums[i]` to the accumulator. O(n) time, O(1) space.
- **In-place prefix sum (cleaner)** — from `i = 1`, do `nums[i] += nums[i-1]`. Each cell already holds the cumulative sum up to `i-1`, so one addition extends it. O(n) time, O(1) space.

## Best solution
```cpp
class Solution {
public:
    vector<int> runningSum(vector<int>& nums) {
        int size = nums.size();
        int i = 1;
        while (i < size) {
            nums[i] += nums[i - 1];
            ++i;
        }
        return nums;
    }
};
```
Optimal because it computes the prefix sum in place with a single addition per element and no temporary variable — the previous cell already carries the accumulated total.

## Notes
- The in-place version is cleaner than tracking a separate accumulator: `nums[i-1]` IS the accumulator once processed.
- This is the canonical prefix-sum build step used as a subroutine in many range-sum problems.

## Techniques
[[Prefix Sum]]

## Sources
- [[1480 Running Sum of 1d Array]] raw note — `raw/notes/DSA/DSA/1480 Running Sum of 1d Array 751545adcc6d45358ed6b3c90ce1bdd8.md`
