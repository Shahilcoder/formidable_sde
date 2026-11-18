---
type: concept
area: sde
title: Bit Packing
aliases: [Bit Packing, Bit Manipulation Packing]
tags: [dsa, arrays, bit-manipulation, in-place]
status: draft
source_count: 1
created: 2026-07-12
updated: 2026-07-12
---

## Summary
Bit Packing stores **two (or more) small values inside a single integer** by shifting one value into the high bits and OR-ing the other into the low bits, then extracting them later with a mask and a shift. It buys you O(1) extra space in problems that would otherwise need a second array to avoid overwriting data you still need. Reach for it when values are bounded (so they fit in a known number of bits) and you must transform an array in place.

## How it works
Pick a bit width `w` large enough to hold each value. To pack value `x` (kept) with value `y` (to be moved):
- **Pack:** `packed = (x << w) | y` — `x` lives in the high bits, `y` in the low `w` bits.
- **Unpack:** `y = packed & ((1 << w) - 1)` (mask the low bits), `x = packed >> w` (shift out the high bits).

Because both originals survive inside one slot, you can rearrange an array without a temporary buffer.

Shuffle the Array in place (LC 1470) — pack `nums[i]` (high) with `nums[n+i]` (low) using a 10-bit width (values ≤ 1000 fit in 10 bits, since 2¹⁰ = 1024), then a backward pass unpacks both halves into their interleaved final positions:
```cpp
vector<int> shuffle(vector<int>& nums, int n) {
    for (int i = 0; i < n; ++i) {
        int y = nums[n + i];              // low value
        nums[i] = (nums[i] << 10) | y;    // pack: x in high bits, y in low 10
    }
    int last = 2 * n - 1;
    for (int j = n - 1; j >= 0; --j) {
        int y = nums[j] & 1023;           // 1023 == (1<<10)-1, mask low 10 bits
        int x = nums[j] >> 10;            // recover high value
        nums[last--] = y;
        nums[last--] = x;
    }
    return nums;
}
```
This turns the naive O(n)-space "copy into a result array" solution into O(1) extra space, still O(n) time. The mask constant `1023` and the shift `10` must agree — both are dictated by the chosen bit width.

## Problems
- [[Shuffle the Array]] (LC 1470) — pack each front value with its back partner in one int (10-bit fields), then unpack backward into interleaved positions for an O(1)-space in-place shuffle.

## Related
[[Index Sign-Marking]] · [[Binary Exponentiation]]

## Sources
- [[Shuffle the Array]] — the two-values-in-one-int packing/unpacking trick with a 10-bit field.
