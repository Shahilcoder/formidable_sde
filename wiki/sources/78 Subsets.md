---
type: source
area: sde
title: 78 Subsets
aliases: [78 Subsets, Subsets]
tags: [dsa, recursion, backtracking]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/78 Subsets 206e9c4cbab88010ae1fe5019989885e.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Given a set of distinct integers, generate its power set (all subsets). The winning idea: backtracking — for each element make a binary decision (skip it / take it), recurse, and undo, collecting a subset at every leaf of the decision tree.

## Approaches
- **Head-recursion power-set build (O(n · 2^n) time and space):** the power set of `k` elements is the power set of `k-1` elements plus a copy of each of those subsets with the `k`th element appended. Recurse down to length 0 (which pushes `{}`), then on the way back up apply this doubling.
- **Backtracking / DFS (O(2^n) time, O(n) space for the recursion stack + current subset):** walk the elements; at each index recurse without picking, then push, recurse with it picked, then pop (undo). Each of the 2^n leaves records one subset.

## Best solution
```cpp
class Solution {
    vector<vector<int>> res;
    vector<int> sol;
    vector<int> payload;

public:
    // Depth first Search.
    void backtrack(int index) {
        // Base Case
        if (index == payload.size()) {
            res.push_back(sol);
            return;
        }

        // Decisions
        // Don't pick the number
        backtrack(index + 1);
        // Nothing to Undo...

        // Pick the number
        sol.push_back(payload[index]);
        backtrack(index + 1);

        // + Undo that decision
        sol.pop_back();
    }

    vector<vector<int>> subsets(vector<int>& nums) {
        res = {};
        sol = {};
        payload = nums;

        backtrack(0);

        return res;
    }
};
```
Optimal in the sense it hits the 2^n lower bound (there are 2^n subsets to output) while carrying only one shared `sol` buffer that is pushed/popped, so extra space beyond the output is O(n).

## Notes
The mental template for backtracking that I noted: make a decision → recurse → hit base case → undo the decision. The "don't pick" branch has nothing to undo; only the "pick" branch needs the matching `pop_back()`. Keyword cue: when a problem says generate **ALL** solutions, reach for backtracking. The head-recursion approach also works but copies the whole result array each level, so it's heavier.

## Techniques
[[Backtracking]]

## Sources
- [[78 Subsets]] raw note — `raw/notes/DSA/DSA/78 Subsets 206e9c4cbab88010ae1fe5019989885e.md`
