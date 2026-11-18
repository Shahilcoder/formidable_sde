---
type: source
area: sde
title: 3289 The Two Sneaky Numbers of Digitville
aliases: [3289 The Two Sneaky Numbers of Digitville, The Two Sneaky Numbers of Digitville]
tags: [dsa, arrays, hashmap, two-pointer]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/3289 The Two Sneaky Numbers of Digitville 29de9c4cbab8804a90b7cedd354f21ac.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Find the two values that appear twice in the array. The linear approach scans once with a hash set, emitting a value the moment it is seen a second time; the alternate sorts and uses adjacent (slow/fast) pointers to spot equal neighbors.

## Approaches
- **Sort + slow/fast two pointers** — sort, then compare each adjacent pair (`nums[slow] == nums[fast]`); a match is a duplicate. O(n log n) time, O(1) space.
- **Hash set with duplicate detection** — insert each number; if it's already present (`s.count(num)`), it's one of the sneaky numbers. O(n) time (average O(1) set ops), O(n) space.

## Best solution
```cpp
class Solution {
public:
    vector<int> getSneakyNumbers(vector<int>& nums) {
        vector<int> answer;
        unordered_set<int> s;

        for (auto num : nums) {
            if (s.count(num)) answer.push_back(num);
            else s.insert(num);
        }

        return answer;
    }
};
```
Optimal in time: a single O(n) pass with average O(1) set lookups, versus the sort approach's O(n log n). Trades O(n) space for the speed.

## Notes
- Exactly two values repeat (each once extra), so the set approach naturally emits exactly two answers.
- The sort + slow/fast variant needs no extra space but pays the sort cost; pick it when memory is tighter than time.

## Techniques
[[Hashmap Lookup Pattern]] · [[Two Pointer Technique]]

## Sources
- [[3289 The Two Sneaky Numbers of Digitville]] raw note — `raw/notes/DSA/DSA/3289 The Two Sneaky Numbers of Digitville 29de9c4cbab8804a90b7cedd354f21ac.md`
