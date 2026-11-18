---
type: source
area: sde
title: 287 Find the Duplicate Number
aliases: [287 Find the Duplicate Number, Find the Duplicate Number]
tags: [dsa, arrays, floyd-cycle-detection, two-pointer]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/287 Find the Duplicate number 125e9c4cbab88045a40ef142744a8a97.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Given `n+1` integers each in `[1, n]`, find the one duplicated value without modifying the array and using O(1) extra space. Treat `i -> nums[i]` as a linked-list "next" pointer; the duplicate creates a cycle, and Floyd's tortoise/hare finds its entrance.

## Approaches
- **Floyd's cycle detection (optimal)** — phase 1: advance `slow` by one and `fast` by two until they meet; phase 2: reset a second pointer to index 0 and advance both by one until they meet again — that meeting point is the cycle entrance = the duplicate. O(n) time, O(1) space.

## Best solution
```cpp
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int slow = 0, fast = 0;

        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (slow != fast);

        int slow2 = 0;
        while (slow != slow2) {
            slow = nums[slow];
            slow2 = nums[slow2];
        }

        return slow;
    }
};
```
Optimal: no auxiliary structure and the input is left untouched, unlike sorting or a hash set.

## Notes
- The note just says "watch NeetCode's video" for the intuition.

> [!note] Claude's addition
> **Why Floyd applies here.** The values lie in `[1, n]` with `n+1` of them, so the map `i -> nums[i]` is a "next pointer" over a functional graph. A repeated value makes two distinct nodes point to the same successor, which forces a cycle. The cycle's ENTRANCE is exactly the duplicated value, because it is the node reached by two different predecessors. Phase 1 (tortoise/hare) finds some meeting point inside the cycle; phase 2, walking one pointer from index `0` and one from the meeting point at equal speed, lands both at the entrance — the duplicate.

## Techniques
[[Floyd's Cycle Detection]]

## Sources
- [[287 Find the Duplicate Number]] raw note — see `raw_path` above.
