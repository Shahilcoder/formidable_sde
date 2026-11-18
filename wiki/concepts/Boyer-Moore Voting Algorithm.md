---
type: concept
area: sde
title: Boyer-Moore Voting Algorithm
aliases: [Boyer-Moore Voting Algorithm, Moore's Voting, Majority Vote Algorithm]
tags: [dsa, arrays, greedy, counting]
status: draft
source_count: 1
created: 2026-07-12
updated: 2026-07-12
---

## Summary
Boyer-Moore Voting finds the **majority element** — a value that appears **more than n/2 times** — in a single pass with O(n) time and O(1) space. Reach for it whenever you need the strict-majority element and want to beat both the O(n) hashmap-counting space and the O(n log n) sort approaches.

## How it works
Keep two variables: a `candidate` and a `vote` counter.

- Start with the first element as `candidate`, `vote = 1`.
- For each subsequent element: `+1` to `vote` if it matches the candidate, `-1` otherwise.
- When `vote` hits `0`, the current candidate has been fully cancelled out — adopt the current element as the new candidate and reset `vote` to `1`.
- After one pass, `candidate` holds the majority element.

```cpp
int majorityElement(vector<int>& nums) {
    int candidate = nums[0], vote = 1;
    for (int i = 1; i < nums.size(); ++i) {
        if (nums[i] == candidate) vote++;
        else vote--;
        if (vote == 0) { candidate = nums[i]; vote = 1; }
    }
    return candidate;
}
```

**Why it works.** The majority appears more than n/2 times, so if you pair up (cancel) each of its occurrences against a *different* element, it still comes out net-positive — there simply aren't enough minority elements to cancel it entirely. The vote counter is exactly this pairing: `+1` for the candidate, `-1` for anything else. Cancellations exhaust the minority elements first, so whatever survives the final reset is the true majority. (If the problem doesn't guarantee a majority exists, a second verification pass counting the candidate's occurrences is needed.)

## Problems
- [[Majority Element]] (LC 169) — canonical use: track candidate + vote, cancel on mismatch, reset on zero; O(1) space beats the hashmap-counting and sorting alternatives the note also records.

## Related
[[Hashmap Lookup Pattern]] · [[Greedy Algorithm]]

## Sources
- [[Majority Element]] — the voting/cancellation strategy and its comparison against hashmap and sort solutions.
