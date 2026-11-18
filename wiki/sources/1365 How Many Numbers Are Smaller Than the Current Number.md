---
type: source
area: sde
title: 1365 How Many Numbers Are Smaller Than the Current Number
aliases: [1365 How Many Numbers Are Smaller Than the Current Number, How Many Numbers Are Smaller Than the Current Number]
tags: [dsa, arrays, prefix-sum, hashmap]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/1365 How many nums are smaller than current num 308e9c4cbab8809c8529ffa22c3e6971.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
For each element, count how many other elements are strictly smaller. The winning idea exploits the tiny value range (0–100): build a tally (count) array, take its prefix sum, and then `answer[i] = prefix[nums[i] - 1]` gives the number of values strictly less than `nums[i]` in O(n).

## Approaches
- **Brute force** — for each `i`, scan all `j` and count `nums[i] > nums[j]`. O(n²) time, O(n) space.
- **Sort + hashmap** — sort a copy; the first index at which a value appears equals the count of smaller values. Map each value to its first index (skip duplicates so they don't overwrite), then rewrite. O(n log n) time, O(n) space.
- **Tally + prefix sum** — count occurrences of each value in a size-101 array, prefix-sum it, then for each `nums[i]` read `prefix[nums[i] - 1]` (0 if value is 0). O(n) time, O(1) extra space when reusing the input array.

## Best solution
```cpp
class Solution {
public:
    vector<int> smallerNumbersThanCurrent(vector<int>& nums) {
        int size = nums.size();
        vector<int> tallyWithPrefixSum(101);

        for (auto number : nums) tallyWithPrefixSum[number]++;

        for (int i = 1; i < 101; ++i)
            tallyWithPrefixSum[i] += tallyWithPrefixSum[i - 1];

        for (int i = 0; i < size; ++i) {
            int position = nums[i];
            if (position == 0) nums[i] = 0;
            else nums[i] = tallyWithPrefixSum[position - 1];
        }

        return nums;
    }
};
```
Optimal because the bounded value range turns a comparison problem into counting: prefix sums give the "how many below" answer in O(1) per element, for O(n) total and O(1) extra space.

## Notes
- The prefix sum at `value - 1` is exactly the number of elements strictly smaller than `value`, because the tally is cumulative.
- Guard `position == 0` to avoid indexing `prefix[-1]`.
- In the sort+hashmap approach, only record the FIRST index for each value so duplicates share the same (correct) smaller-count.

## Techniques
[[Prefix Sum]] · [[Hashmap Lookup Pattern]] · [[Coordinate Compression]]

## Sources
- [[1365 How Many Numbers Are Smaller Than the Current Number]] raw note — `raw/notes/DSA/DSA/1365 How many nums are smaller than current num 308e9c4cbab8809c8529ffa22c3e6971.md`
