---
type: source
area: sde
title: 31 Next Permutation
aliases: [31 Next Permutation, Next Permutation]
tags: [dsa, arrays, greedy]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/31 Next Permutation 106e9c4cbab88027bdf0e691e74bc2ae.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Rearrange numbers into the lexicographically next greater permutation in place. Scan from the back for the first "dip" (`nums[i] < nums[i+1]`); swap it with the next-larger element to its right, then reverse the suffix to make it the smallest possible ordering.

## Approaches
- **Linear three-pass** — (1) from the back, find the pivot/dip index where the sequence stops increasing; (2) if none exists, the array is the largest permutation, so reverse the whole thing; (3) otherwise find the rightmost element greater than the pivot, swap them, and reverse the suffix after the pivot. Time O(n), space O(1).

## Best solution
```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int size = nums.size();
        int index = -1;

        // find the dip from back, from n-2
        for (int i = size - 2; i >= 0; --i) {
            if (nums[i] < nums[i + 1]) {
                index = i;
                break;
            }
        }

        // if no dip, it's the largest permutation
        if (index == -1) {
            reverse(nums.begin(), nums.end());
            return;
        }

        // find, from back, the element just greater than the dip
        for (int i = size - 1; i > index; --i) {
            if (nums[i] > nums[index]) {
                swap(nums[i], nums[index]);
                break;
            }
        }

        // reverse the suffix after the dip to keep it minimum
        reverse(nums.begin() + index + 1, nums.end());
    }
};
```
Optimal because it computes the answer in place with a constant number of linear scans — no sorting, no extra memory.

## Notes
- The greedy insight: to get the *next* larger permutation you change the value as far right (least significant) as possible, and after the single swap the suffix is already descending, so reversing it yields the smallest tail.
- The suffix after the pivot is guaranteed non-increasing, so `reverse` alone sorts it ascending — no full sort needed.
- Complexity noted as O(3n) → O(n).

## Techniques
[[Greedy Algorithm]] · [[In-place Array Reversal]]

## Sources
- [[31 Next Permutation]] raw note — `raw/notes/DSA/DSA/31 Next Permutation 106e9c4cbab88027bdf0e691e74bc2ae.md`
