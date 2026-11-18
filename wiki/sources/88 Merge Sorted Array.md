---
type: source
area: sde
title: 88 Merge Sorted Array
aliases: [88 Merge Sorted Array, Merge Sorted Array]
tags: [dsa, arrays, two-pointer]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/88 Merge sorted array a7b41dbe4cf04fdf9fa5b7ada5a80406.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Merge two sorted arrays `nums1` (with `n` trailing empty slots) and `nums2` into `nums1` in sorted order. The winning idea: run the merge-sort merge **in reverse**, filling `nums1` from the back with the largest elements so you never overwrite unread `nums1` values.

## Approaches
- **Concatenate + sort (O((m+n) log(m+n)) time, O(1) space):** copy `nums2` into the tail of `nums1` and call `sort`. Simple, but ignores that both inputs are already sorted.
- **Reverse three-pointer merge (O(m+n) time, O(1) space):** pointers `i` at end of `nums1`'s real data, `j` at end of `nums2`, `k` at the very end of `nums1`. Write the larger of `nums1[i]`/`nums2[j]` into `nums1[k]` and step back, then drain whatever remains.

## Best solution
```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i = m - 1, j = n - 1, k = m + n - 1;

        while (i >= 0 && j >= 0) {
            if (nums1[i] >= nums2[j]) nums1[k--] = nums1[i--];
            else nums1[k--] = nums2[j--];
        }

        while (i >= 0) nums1[k--] = nums1[i--];
        while (j >= 0) nums1[k--] = nums2[j--];
    }
};
```
Optimal because filling from the back reuses the free tail space, so it merges in a single linear pass with no extra array and no sort.

## Notes
The key trick is *reverse* merging. A forward merge into `nums1` would clobber elements of `nums1` you haven't read yet; going back-to-front means every slot you write (`k`) is at or beyond both read pointers, so the source data is always safe. Only the leftover `nums2` tail needs draining — leftover `nums1` elements are already in place.

## Techniques
[[Two Pointer Technique]]

## Sources
- [[88 Merge Sorted Array]] raw note — `raw/notes/DSA/DSA/88 Merge sorted array a7b41dbe4cf04fdf9fa5b7ada5a80406.md`
