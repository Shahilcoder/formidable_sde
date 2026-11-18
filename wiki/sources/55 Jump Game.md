---
type: source
area: sde
title: 55 Jump Game
aliases: [55 Jump Game, Jump Game]
tags: [dsa, arrays, greedy]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/55 Jump Game 12de9c4cbab8806e8c13f3a1491d3c03.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Given an array where each `nums[i]` is the max jump length from index `i`, decide whether you can reach the last index starting from index 0. The winning idea is a greedy backward scan: track a moving "goal" post; if reachable from the front, `goal` collapses to 0.

## Approaches
- **Backward zero-hunt (O(n) time, O(1) space):** walk from the second-last index backward; whenever a `0` is found, scan further back for any element that can jump over it. If no such element exists, return false. Works but has a nested scan.
- **Greedy backward goal (O(n) time, O(1) space):** start with `goal = last index`. Scanning right-to-left, if `i + nums[i] >= goal`, the goal can be reached from `i`, so move `goal = i`. If `goal` reaches 0, index 0 can reach the end.

## Best solution
```cpp
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int size = nums.size();

        int goal = size - 1;

        for (int i = size - 2; i >= 0; --i) {
            if (i + nums[i] >= goal) goal = i;
        }

        if (goal == 0) return true;
        return false;
    }
};
```
Optimal because it makes one backward pass with O(1) state: each index only needs to know if it can reach the current goal, greedily pulling the goal leftward.

## Notes
The first solution I wrote hunts for zeros and back-scans to see if they can be jumped over — correct, but the nested scan makes it feel more complex than it is. The greedy goal-post reframing (from NeetCode) is much cleaner: instead of asking "which zeros trap me", ask "how far left can the reach-the-end goal migrate".

## Techniques
[[Greedy Algorithm]]

## Sources
- [[55 Jump Game]] raw note — `raw/notes/DSA/DSA/55 Jump Game 12de9c4cbab8806e8c13f3a1491d3c03.md`
