---
type: source
area: sde
title: 1470 Shuffle the Array
aliases: [1470 Shuffle the Array, Shuffle the Array]
tags: [dsa, arrays, bit-packing]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/1470 Shuffle the array 2f0e9c4cbab8800387f5eaceda5aeb7f.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Given `nums = [x1..xn, y1..yn]`, interleave to `[x1,y1,x2,y2,...]`. The straightforward answer writes into a fresh output array in O(n) space; the clever answer packs each pair `(xi, yi)` into a single int using bit shifts, then unpacks in reverse to rearrange fully in place with O(1) extra space.

## Approaches
- **Fresh output array** — walk `i` from 0 to `n`, pushing `nums[i]` then `nums[i+n]` (or writing into a preallocated `result(2*n)` with two cursors). O(n) time, O(n) space.
- **Bit-packing trick** — since each value fits in 10 bits, store `x` in the high bits and `y` in the low 10 bits of `nums[i]` (`nums[i] = (nums[i] << 10) | nums[n+i]`). Then walk from the back, extract `y = nums[j] & 1023` and `x = nums[j] >> 10`, and place them at the correct interleaved positions. O(n) time, O(1) space.

## Best solution
```cpp
class Solution {
public:
    vector<int> shuffle(vector<int>& nums, int n) {
        for (int i = 0; i < n; ++i) {
            nums[i] = nums[i] << 10;   // x in high bits
            int y = nums[n + i];
            nums[i] = nums[i] | y;     // y in low 10 bits
        }

        int last = 2 * n - 1;
        for (int j = n - 1; j >= 0; --j) {
            int y = nums[j] & 1023;    // low 10 bits
            int x = nums[j] >> 10;     // high bits
            nums[last--] = y;
            nums[last--] = x;
        }
        // guaranteed last == -1 at the end
        return nums;
    }
};
```
Optimal in space: it reuses the input array as scratch by co-locating two 10-bit values in one 32-bit int, achieving the interleave with no auxiliary allocation.

## Notes
- Works because constraints bound `nums[i] <= 1000 < 2^10`, so 10 bits suffice per value and both fit in one int.
- Unpack from the back so you never overwrite a still-packed cell before reading it.
- The mask `1023 = 2^10 - 1` isolates the low 10 bits (`y`); the `>> 10` recovers `x`.

## Techniques
[[Bit Packing]]

## Sources
- [[1470 Shuffle the Array]] raw note — `raw/notes/DSA/DSA/1470 Shuffle the array 2f0e9c4cbab8800387f5eaceda5aeb7f.md`
