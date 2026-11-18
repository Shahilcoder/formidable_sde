---
type: pattern
area: sde
title: Index Sign-Marking
aliases: [Index Sign-Marking, Negation Trick, Value-as-Index Marking]
tags: [dsa, arrays, in-place, hashing]
status: draft
source_count: 2
created: 2026-07-12
updated: 2026-07-12
---

## Summary
When an array holds values in the range `[1, n]` (or `[0, n-1]`), you can use the array **itself** as a presence map instead of an external hash set. Mark "value `v` has been seen" by flipping the **sign** of the element at index `v - 1`. This gives you O(1) extra space where the natural hashmap solution needs O(n). Reach for it on "find the missing / duplicate numbers in a bounded-range array" problems where the interviewer asks for constant space.

## How it works
The trick relies on two facts: values are 1-indexable into the array, and sign is a spare bit of information the values don't otherwise use (they're all positive to begin with).

1. **Mark pass** — for each element, take `idx = abs(v) - 1` (use `abs` because a slot may already be negated by an earlier value) and negate `nums[idx]`. A negative slot at index `i` now means "value `i + 1` was present."
2. **Read pass** — walk the array. Any index `i` whose value is still **positive** was never marked, so `i + 1` never appeared. A slot found **already negative** during the mark pass signals a duplicate.

Reading via `abs()` is essential: once you start negating, the raw stored value can no longer be trusted for its magnitude alone — only `abs(v)` is meaningful.

Canonical missing-numbers snippet (LC 448):
```cpp
vector<int> findDisappearedNumbers(vector<int>& nums) {
    for (int v : nums) {
        int idx = abs(v) - 1;
        if (nums[idx] > 0) nums[idx] = -nums[idx];   // mark "idx+1 present"
    }
    vector<int> ans;
    for (int i = 0; i < nums.size(); ++i)
        if (nums[i] > 0) ans.push_back(i + 1);        // still positive → missing
    return ans;
}
```

Set-mismatch variant (LC 645) finds both the duplicate and the missing number in one structure: if a slot is *already* negative when you try to mark it, the value that maps there is the duplicate; the slot still positive after the mark pass gives the missing number.

## Problems
- [[Find All Numbers Disappeared in an Array]] (LC 448) — negate `nums[abs(v)-1]`; indices left positive give the missing values in O(1) space. The user's note only had the hashmap approach; the sign-marking version is added there as the canonical solution.
- [[Set Mismatch]] (LC 645) — same negation, but an already-negative slot reveals the duplicate while the still-positive slot reveals the missing number.

## Related
[[Hashmap Lookup Pattern]] · [[Boyer-Moore Voting Algorithm]]

## Sources
- [[Find All Numbers Disappeared in an Array]] — bounded-range missing-numbers marking.
- [[Set Mismatch]] — extending the negation trick to report duplicate + missing together.
