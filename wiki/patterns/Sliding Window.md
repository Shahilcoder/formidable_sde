---
type: pattern
area: sde
title: Sliding Window
aliases: [Sliding Window]
tags: [dsa, arrays, sliding-window]
status: draft
source_count: 2
created: 2026-07-12
updated: 2026-07-14
---

## Summary
Maintain a contiguous window over an array and update its aggregate (sum, count, max, …) incrementally as the window moves, instead of recomputing over the whole window each step. Reach for it on "best/longest/shortest contiguous subarray/substring of size k (or satisfying a condition)" problems. A fixed-size window turns an O(n·k) recomputation into O(n): each step you subtract the element leaving and add the element entering.

## How it works
For a fixed window of width `k`: seed the aggregate over the first valid window, then slide one step at a time, adjusting by the delta at each edge.

```cpp
// window over the LAST k cards, slid leftward across a circular choice
int r = size - k, max_sum = 0;
for (int i = r; i < size; ++i) max_sum += cardPoints[i];   // seed
int totalSum = max_sum;
while (r < size) {
    totalSum = totalSum - cardPoints[r++] + cardPoints[l++]; // element out, element in
    max_sum = max(totalSum, max_sum);
}
```

The trick in [[Maximum Points You Can Obtain from Cards]]: picking `k` cards from the two ends is equivalent to leaving a contiguous window of `n-k` in the middle, so *maximizing the ends = minimizing the middle window* — reframed as a fixed-size window over the array. O(k) time, O(1) space.

## Problems
- [[Maximum Points You Can Obtain from Cards]] (LC 1423) — pick k cards from either end; slide a size-(n-k) window and track the max total taken from the ends.
- [[1291 Sequential Digits]] (LC 1291) — a lighter, "enumeration" flavor: slide a fixed-width window across the constant string `"123456789"` to generate every sequential-digit number. No incremental aggregate here (each window is re-read); the real driver is the tiny fixed catalog — see [[Bounded Solution Space]].

## Related
[[Two Pointer Technique]] · [[Prefix Sum]] · [[Bounded Solution Space]]

## Sources
- [[Maximum Points You Can Obtain from Cards]] — fixed-size window, incremental sum update
- [[1291 Sequential Digits]] — fixed-width window slid over a constant string to enumerate candidates
