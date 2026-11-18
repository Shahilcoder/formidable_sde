---
type: source
area: sde
title: 45 Jump Game II
aliases: [45 Jump Game II, Jump Game II]
tags: [dsa, arrays, greedy]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/45 Jump Game II 133e9c4cbab880c895b5cd34a9914d39.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Find the minimum number of jumps to reach the last index, where `nums[i]` is the max jump length from `i`. The note's greedy approach works backwards: from the current goal, find the leftmost index that can reach it, make that the new goal, and count one jump per hop.

## Approaches
- **Greedy backward** — start with `goal = last index`. Scan leftward for the smallest index `i` that can reach the goal (`i + nums[i] >= goal`); set the goal to that index and increment the jump count. Repeat until the goal is 0. Time O(n) amortized, space O(1).

## Best solution
```cpp
class Solution {
public:
    int jump(vector<int>& nums) {
        int size = nums.size();
        int goal = size - 1;
        int jumps = 0;

        int max_index = goal;
        while (goal > 0) {
            int i = max_index - 1;

            while (i >= 0) {
                if (i + nums[i] >= goal) {
                    max_index = min(i, max_index);
                }

                --i;
            }

            jumps++;
            goal = max_index;
        }

        return jumps;
    }
};
```
Optimal in space and (per the note's LeetCode check) linear in time. Framed as an extension of NeetCode's Jump Game I greedy reachability idea.

## Notes
- The note observes the runtime shrinks each outer pass (roughly 1n, 0.5n, 0.23n...) which still amortizes to O(n).
- The classic forward "BFS-style" greedy — tracking `currentEnd` and `farthest`, bumping jumps when you pass the current window — is the more common O(n) formulation; this backward version reaches the same count.
- Always solvable (the problem guarantees the last index is reachable), so no unreachable case is handled.

## Techniques
[[Greedy Algorithm]]

## Sources
- [[45 Jump Game II]] raw note — `raw/notes/DSA/DSA/45 Jump Game II 133e9c4cbab880c895b5cd34a9914d39.md`
