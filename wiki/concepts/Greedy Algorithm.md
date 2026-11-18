---
type: concept
area: sde
title: Greedy Algorithm
aliases: [Greedy Algorithm, Greedy]
tags: [dsa, arrays, greedy]
status: draft
source_count: 7
created: 2026-07-12
updated: 2026-07-12
---

## Summary
A greedy algorithm builds a solution by making the locally optimal choice at each step, never revisiting past decisions, and trusts that these local optima compose into a global optimum. It applies only when the problem has the **greedy-choice property** (a local best is safe) and **optimal substructure**. When it works it is typically O(n) time and O(1) space — dramatically simpler than the DP alternative — but proving the greedy choice is safe is the real work. Common tells in the user's set: "maximize profit", "minimum jumps", "merge overlapping", "max gap after sorting".

## How it works
The pattern is: scan once, keep a running "best so far" or a moving frontier/goal, and fold each element into it with a `min`/`max`/comparison — no backtracking.

Best Time to Buy and Sell Stock keeps the minimum price seen and the best profit against it:

```cpp
int max_profit = 0, min_price = INT_MAX;
for (int p : prices) {
    min_price  = min(min_price, p);
    max_profit = max(max_profit, p - min_price);
}
```

Jump Game walks a `goal` frontier backward: if index `i` can reach the current goal, `i` becomes the new goal; reaching index 0 means the end is reachable. A frequent enabler is **sorting first** so that the greedy choice becomes obvious on adjacent elements (Merge Intervals, Maximum Area of a Piece of Cake).

## Problems
- [[Next Permutation]] (LC 31) — greedily pick the *smallest* increase: swap the dip with its next-greater successor, then minimize the suffix.
- [[Jump Game II]] (LC 45) — greedily pull the reachable frontier back to the earliest index that still reaches the goal, counting jumps.
- [[Jump Game]] (LC 55) — sweep a `goal` backward; if it collapses to index 0, the end is reachable.
- [[Merge Intervals]] (LC 56) — sort by start, then greedily extend the last merged interval or start a new one.
- [[Best Time to Buy and Sell Stock]] (LC 121) — track running min price and best profit against it in one pass.
- [[Best Time to Buy and Sell Stock II]] (LC 122) — greedily bank every upward step `prices[i+1] - prices[i]` (telescopes to the true max).
- [[Maximum Area of a Piece of Cake]] (LC 1465) — sort cuts, greedily take the largest adjacent gap on each axis, multiply.

## Related
[[Two Pointer Technique]] · [[In-place Array Reversal]]

## Sources
- [[Next Permutation]] — smallest-lexicographic-increase greedy choice
- [[Jump Game II]] — minimum jumps via a receding frontier
- [[Jump Game]] — backward goal collapse
- [[Merge Intervals]] — sort-then-merge greedy sweep
- [[Best Time to Buy and Sell Stock]] — running min + best profit
- [[Best Time to Buy and Sell Stock II]] — sum every positive delta
- [[Maximum Area of a Piece of Cake]] — max adjacent gap after sorting
