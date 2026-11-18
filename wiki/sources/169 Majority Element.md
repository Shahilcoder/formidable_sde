---
type: source
area: sde
title: 169 Majority Element
aliases: [169 Majority Element, Majority Element]
tags: [dsa, arrays, hashmap]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/169 Majority Element dcdedc9b9c154d41a6e2b1f8d896b49f.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Find the element that appears more than ⌊n/2⌋ times in an array. The winning idea: Boyer-Moore voting — maintain one candidate and a counter, cancelling opposing votes, so the true majority is the last one standing in O(1) space.

## Approaches
- **Hashmap frequency count (O(n) time, O(n) space):** tally counts; the moment a count exceeds n/2, return that element.
- **Sort and take the middle (O(n log n) time, O(1) space):** after sorting, the element at index n/2 must be the majority since it occupies more than half the slots.
- **Boyer-Moore voting (O(n) time, O(1) space):** keep a candidate and a vote count; +1 when the current element matches, -1 otherwise; when the count hits 0, adopt the current element as the new candidate.

## Best solution
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int size = nums.size();
        int candidate = nums[0];
        int vote = 1;

        for (int i = 1; i < size; ++i) {
            if (candidate == nums[i]) vote++;
            else vote--;

            if (vote == 0) {
                candidate = nums[i];
                vote++;
            }
        }

        return candidate;
    }
};
```
Optimal because it solves the problem in one pass with O(1) space — no auxiliary map and no sort.

## Notes
Why voting works: the majority appears more than n/2 times, so pairing off each of its occurrences against a different element still leaves it net-positive. The counter cancels minority elements against each other (and against the majority), and because minorities are fewer they exhaust first, so the true majority survives as the final candidate. The problem guarantees a majority exists, so no verification pass is needed.

## Techniques
[[Boyer-Moore Voting Algorithm]] · [[Hashmap Lookup Pattern]]

## Sources
- [[169 Majority Element]] raw note — `raw/notes/DSA/DSA/169 Majority Element dcdedc9b9c154d41a6e2b1f8d896b49f.md`
