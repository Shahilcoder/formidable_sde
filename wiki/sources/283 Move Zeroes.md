---
type: source
area: sde
title: 283 Move Zeroes
aliases: [283 Move Zeroes, Move Zeroes]
tags: [dsa, arrays, two-pointer]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/283 Move Zeros a9033478891246d7b07d808936055bf9.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Move all `0`s in an array to the end while keeping the relative order of the non-zero elements, in place. The winning idea is a slow/fast two-pointer pass: `fast` scans, and every non-zero value is written forward at `slow`; a final pass zero-fills the tail.

## Approaches
- **Zero-bubble sort** — bubble the zeros toward the end by swapping adjacent pairs. O(n^2) time, O(1) space.
- **Slow/fast two pointers (optimal)** — `fast` scans the array; whenever `nums[fast] != 0`, copy it to `nums[slow++]`. After the scan, fill `slow..end` with `0`. O(n) time, O(1) space.

## Best solution
```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int len = nums.size();
        int slow = 0;
        // keep fast = 0; starting fast = 1 fails the case [1, 0]
        int fast = 0;

        while (fast < len) {
            if (nums[fast] != 0) nums[slow++] = nums[fast];
            fast++;
        }

        while (slow < len) nums[slow++] = 0;
    }
};
```
Optimal: a single O(n) pass writes non-zeros forward preserving order, and the trailing zero-fill needs no extra space.

## Notes
- Gotcha recorded in the note: start `fast` at `0`, not `1`. Starting at `1` fails `[1, 0]`.

## Techniques
[[Two Pointer Technique]]

## Sources
- [[283 Move Zeroes]] raw note — see `raw_path` above.
