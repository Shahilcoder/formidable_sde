---
type: source
area: sde
title: 1 Two Sum
aliases: [1 Two Sum, Two Sum]
tags: [dsa, arrays, hashmap, two-pointer]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/1 Two Sum adb69b457375414f8338198e99f9b8fb.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Given an array and a target, return the indices of the two numbers that sum to the target. The winning idea is a single-pass hash map: for each element, look up whether its complement `target - nums[i]` has already been seen in O(1).

## Approaches
- **Brute force** — nested loop checking every pair. Time O(n²), space O(1).
- **Hash map** — store `value → index`, then for each element look up the complement. Time O(n), space O(n). This is the optimal general solution (works on unsorted input, returns original indices).
- **Sort + two pointer** — build pairs of `(value, index)`, sort by value, converge from both ends. Time O(n log n), space O(n). Loses the O(n) advantage because of the sort, but useful when indices don't matter.

## Best solution
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        if (nums.size() == 2) return {0, 1};

        unordered_map<int, int> map;

        for (int i = 0; i < nums.size(); ++i) map[nums[i]] = i;

        for (int i = 0; i < nums.size(); ++i) {
            int to_search = target - nums[i];

            if (auto check = map.find(to_search); check != map.end() && check->second != i)
                return {i, check->second};
        }

        return {-1, -1};
    }
};
```
Optimal because the hash lookup turns the inner O(n) scan into O(1) average, giving one linear pass over the array while preserving the original indices.

## Notes
- The `check->second != i` guard prevents matching an element with itself (e.g. `target = 2*nums[i]`).
- The note stores every element first, then scans; a tighter one-pass variant inserts as it goes so the self-match is impossible by construction.
- The two-pointer variant requires sorting, which destroys original indices — hence it stores `(value, index)` pairs.

## Techniques
[[Hashmap Lookup Pattern]] · [[Two Pointer Technique]] · [[k-Sum Pattern]]

## Sources
- [[1 Two Sum]] raw note — `raw/notes/DSA/DSA/1 Two Sum adb69b457375414f8338198e99f9b8fb.md`
