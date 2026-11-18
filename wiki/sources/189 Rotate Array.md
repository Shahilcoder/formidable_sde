---
type: source
area: sde
title: 189 Rotate Array
aliases: [189 Rotate Array, Rotate Array]
tags: [dsa, arrays, in-place]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/189 Rotate Array 15de9c4cbab88090a4bddbb8a365cd13.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Rotate an array to the right by `k` steps. The winning idea: reverse the whole array, then reverse the first `k` and the remaining `n-k` elements separately — three reversals give an in-place O(1)-space rotation.

## Approaches
- **Extra array with modular placement (O(n) time, O(n) space):** write each `nums[i]` to `result[(i+k) % size]`, then copy back.
- **Queue-assisted shifting (O(n) time, O(n) space):** shuffle elements into their rotated positions using a queue to buffer displaced values.
- **Reverse-reverse-reverse (O(n) time, O(1) space):** normalize `k %= size`, reverse the entire array, then reverse `[0, k)` and `[k, n)`.

## Best solution
```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int size = nums.size();
        // k can be greater than or equal to size of the array
        // rather than useless rotations, chop it off to useful rotations
        k = k % size;

        reverse(nums.begin(), nums.end());
        reverse(nums.begin(), nums.begin() + k);
        reverse(nums.begin() + k, nums.end());
    }
};
```
Optimal because it rotates in place with O(1) extra space; the three linear reversals total O(n) time with no auxiliary array.

## Notes
The `k %= size` normalization is essential — `k` can exceed the array length, and rotating by full multiples of `size` is a no-op, so reducing avoids wasted work and out-of-range reversal boundaries. Intuition for the three reversals: reversing the whole array brings the last `k` elements to the front but in reverse order; reversing each of the two segments fixes their internal order.

## Techniques
[[In-place Array Reversal]]

## Sources
- [[189 Rotate Array]] raw note — `raw/notes/DSA/DSA/189 Rotate Array 15de9c4cbab88090a4bddbb8a365cd13.md`
