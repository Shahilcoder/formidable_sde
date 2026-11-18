---
type: source
area: sde
title: 560 Subarray Sum Equals K
aliases: [560 Subarray Sum Equals K, Subarray Sum Equals K]
tags: [dsa, arrays, prefix-sum, hashmap]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/560 Subarray sum equals k 423175f258b34831abf69f44a887fa21.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Count the number of contiguous subarrays whose sum equals `k`. Maintain a running prefix sum and a hash map of how many times each prefix sum has occurred; at each step, the count of earlier prefix sums equal to `prefixSum - k` is exactly the number of subarrays ending here that sum to `k`.

## Approaches
- **Prefix sum + hash map (optimal)** — for each running prefix sum `s`, add `mp[s - k]` to the answer (subarrays ending at the current index summing to `k`), then record `s` in the map. Seed the map with `mp[0] = 1` so subarrays starting at index 0 are counted. O(n) time, O(n) space.

## Best solution
```cpp
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int size = nums.size();
        unordered_map<int, int> mp;
        int count = 0, prefixSum = 0;
        mp[prefixSum] = 1;

        for (auto e: nums) {
            prefixSum += e;
            count += mp[prefixSum - k];
            mp[prefixSum]++;
        }

        return count;
    }
};
```
Optimal: a single pass, replacing an O(n^2) recount of every subarray with O(1) hash lookups.

## Notes
- Critical detail from the note: initialize `mp[0] = 1`. If `s == k`, then `s - k == 0`, and that seeded entry lets the whole prefix be counted as a valid subarray even when no other prefix sum of `0` exists.

## Techniques
[[Prefix Sum]] · [[Hashmap Lookup Pattern]]

## Sources
- [[560 Subarray Sum Equals K]] raw note — see `raw_path` above.
