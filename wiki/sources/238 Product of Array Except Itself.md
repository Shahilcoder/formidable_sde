---
type: source
area: sde
title: 238 Product of Array Except Itself
aliases: [238 Product of Array Except Itself, Product of Array Except Itself]
tags: [dsa, arrays, prefix-sum]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/238 Product of Array Except Itself 2fe013f305c845888671a7ddf57ee81c.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
For each index, return the product of all other elements — without division. The winning idea: a prefix-product / suffix-product sweep, storing the running prefix in the result, then multiplying by the running suffix on a backward pass.

## Approaches
- **Two separate passes (O(n) time, O(n) output):** first pass fills `res[i]` with the product of everything before `i` (running prefix `p`). Second pass multiplies `res[i]` by the product of everything after `i` (running suffix `p`).
- **Single fused loop (O(n) time, O(n) output):** carry two running products `p1` (front) and `p2` (back) and update `res[i]` and `res[size-1-i]` in the same iteration.

## Best solution
```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int size = nums.size();
        int p = 1;

        vector<int> res(size, 0);

        for (int i = 0; i < size; ++i) {
            res[i] = p;
            p *= nums[i];
        }

        p = 1;
        for (int i = size - 1; i >= 0; --i) {
            res[i] *= p;
            p *= nums[i];
        }

        return res;
    }
};
```
Optimal because it avoids division and uses only the output array plus one scalar — the prefix products are stashed in `res` on the way forward, then combined with suffix products on the way back. (The note's fused single-loop variant does the same in one pass.)

## Notes
The trick is that you never need to store a full prefix array and a full suffix array separately: write the prefix products into `res` first, then a second running product from the right folds the suffixes into the same array. `res[i]` momentarily holds "product of all before i", and after the backward pass it holds "before × after" = everything except itself.

## Techniques
[[Prefix Sum]]

## Sources
- [[238 Product of Array Except Itself]] raw note — `raw/notes/DSA/DSA/238 Product of Array Except Itself 2fe013f305c845888671a7ddf57ee81c.md`
