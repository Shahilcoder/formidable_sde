---
type: source
area: sde
title: 1752 Check if Array Is Sorted and Rotated
aliases: [1752 Check if Array Is Sorted and Rotated, Check if Array Is Sorted and Rotated]
tags: [dsa, arrays, array]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/1752 Check if array is sorted and rotated 15ce9c4cbab88097a25fea7d7226937f.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Decide whether an array is a (possibly zero-shift) rotation of a non-decreasing array. A sorted-then-rotated array has at most one "drop" point where an element exceeds its successor when you scan circularly; count those drops, and if there's more than one, it's not valid.

## Approaches
- **Circular single traversal** — count how many times `nums[i] > nums[(i+1) % size]`. The `% size` wraps the last element around to compare against the first. If the count exceeds 1, return false; otherwise true. O(n) time, O(1) space.

## Best solution
```cpp
class Solution {
public:
    bool check(vector<int>& nums) {
        int size = nums.size();
        int count = 0;

        for (int i = 0; i < size; ++i) {
            if (nums[i] > nums[(i + 1) % size]) count++;
            if (count > 1) return false;
        }

        return true;
    }
};
```
Optimal because a sorted array rotated by some amount has exactly one wrap-around descent (or zero if unrotated); a single circular pass detects that in linear time and constant space.

## Notes
- Only the sorted property matters; the "rotated" claim needs no verification because any array with ≤1 circular drop is a rotation of a sorted array.
- The `(i+1) % size` comparison of last-vs-first is what makes the single pass sufficient — no need to actually loop the array around more than once.

## Sources
- [[1752 Check if Array Is Sorted and Rotated]] raw note — `raw/notes/DSA/DSA/1752 Check if array is sorted and rotated 15ce9c4cbab88097a25fea7d7226937f.md`
