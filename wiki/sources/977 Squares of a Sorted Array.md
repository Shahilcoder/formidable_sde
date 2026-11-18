---
type: source
area: sde
title: 977 Squares of a Sorted Array
aliases: [977 Squares of a Sorted Array, Squares of a Sorted Array]
tags: [dsa, arrays, two-pointer]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/977 Squares of sorted Array 7a8d7023c8284a5f904f897ef9d094e7.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Given a sorted array (with negatives), return the squares in sorted order. Since the largest square must be at one of the two ends, use two pointers from both ends and fill the result array back to front with the larger square.

## Approaches
- **Two pointers filling back to front (optimal)** — pointers `l` at the start and `r` at the end; compare `abs(nums[l])` vs `abs(nums[r])`, write the larger square at the current back position `k` of the result, and move the corresponding pointer inward. O(n) time, O(n) space.

## Best solution
```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        int size = nums.size();
        vector<int> res(size);

        int l = 0, r = size - 1, k = size - 1;

        while (k >= 0) {
            if (abs(nums[l]) > abs(nums[r])) res[k--] = nums[l] * nums[l], l++;
            else res[k--] = nums[r] * nums[r], r--;
        }

        return res;
    }
};
```
Optimal: a single O(n) pass exploits the existing sort, avoiding the O(n log n) of squaring then re-sorting.

## Notes
- Key insight: the maximum absolute value (hence maximum square) is always at one of the two ends, so filling the result from the back keeps it sorted.

## Techniques
[[Two Pointer Technique]]

## Sources
- [[977 Squares of a Sorted Array]] raw note — see `raw_path` above.
