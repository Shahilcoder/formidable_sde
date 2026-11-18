---
type: source
area: sde
title: 26 Remove Duplicates from Sorted Array
aliases: [26 Remove Duplicates from Sorted Array, Remove Duplicates from Sorted Array]
tags: [dsa, arrays, two-pointer]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/26 Remove duplicates for sorted array 8a5310b98e034749a7ae04aa361fbd7e.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Remove duplicates in place from a sorted array and return the new length. A slow/fast two-pointer walk: `fast` scans every element, and whenever it finds a value different from its predecessor, `slow` writes it into the compacted prefix.

## Approaches
- **Slow/fast two pointer** — `fast` scans from index 1; when `nums[fast-1] != nums[fast]` (a new distinct value), copy it to `nums[slow]` and advance `slow`. `slow` ends as the count of unique elements. Time O(n), space O(1).

## Best solution
```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int size = nums.size();

        int slow = 1;
        int fast = 1;

        while (fast < size) {
            if (nums[fast - 1] != nums[fast]) {
                nums[slow++] = nums[fast];
            }

            fast++;
        }

        return slow;
    }
};
```
Optimal because it's a single linear pass that compacts in place — no extra storage, and the sorted input guarantees duplicates are adjacent so comparing to the previous element suffices.

## Notes
- Both pointers start at 1 since index 0 is always a kept element.
- The comparison is against `nums[fast-1]` (the previous scanned value), which works precisely because the array is sorted — duplicates cluster together.
- `slow` doubles as both the write cursor and the final unique count.

## Techniques
[[Two Pointer Technique]]

## Sources
- [[26 Remove Duplicates from Sorted Array]] raw note — `raw/notes/DSA/DSA/26 Remove duplicates for sorted array 8a5310b98e034749a7ae04aa361fbd7e.md`
