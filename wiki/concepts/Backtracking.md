---
type: concept
area: sde
title: Backtracking
aliases: [Backtracking, Recursive Backtracking]
tags: [dsa, recursion, backtracking, dfs]
status: draft
source_count: 1
created: 2026-07-12
updated: 2026-07-12
---

## Summary
Backtracking is a systematic way to **generate ALL solutions** (subsets, permutations, combinations, board placements) by building a partial solution incrementally and undoing each choice after exploring it. It's a depth-first search over an implicit decision tree. Reach for it whenever the ask is "generate/enumerate all …" and the search space branches on a sequence of choices.

## How it works
The core loop is four steps repeated recursively:

1. **Decide** — make a choice (include this element, place this queen, pick this digit).
2. **Recurse** — descend to the next decision with that choice applied.
3. **Base case** — when there are no decisions left, record the completed solution.
4. **Undo** — revert the choice (pop it back off) so the next branch starts clean.

That undo step is what makes it *backtracking*: a single mutable path buffer is shared across the whole tree, pushed on the way down and popped on the way back up, so you never pay to copy state per branch.

Subsets via backtracking (LC 78) — at each index, branch on "skip it" vs "take it":
```cpp
vector<vector<int>> res;
vector<int> sol, nums;

void backtrack(int index) {
    if (index == nums.size()) {      // base case: a complete decision path
        res.push_back(sol);
        return;
    }
    backtrack(index + 1);            // decision: don't pick nums[index]

    sol.push_back(nums[index]);      // decision: pick nums[index]
    backtrack(index + 1);
    sol.pop_back();                  // undo
}
```

For `n` elements each with a binary include/exclude choice, this explores 2ⁿ leaves — O(2ⁿ) time and O(n) recursion depth (the shared `sol` buffer). Pruning invalid branches early (e.g. constraint violations) is the main lever for making backtracking tractable on harder problems.

## Problems
- [[Subsets]] (LC 78) — decide skip-vs-take at each index, recurse, record at the leaf, then pop to undo; the DFS over the include/exclude tree enumerates all 2ⁿ subsets.

## Related
[[Binary Exponentiation]] · [[Bit Packing]]

## Sources
- [[Subsets]] — the decide→recurse→base→undo framing and the include/exclude DFS.
