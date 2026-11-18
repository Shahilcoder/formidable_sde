---
type: source
area: sde
title: 448 Find All Numbers Disappeared in an Array
aliases: [448 Find All Numbers Disappeared in an Array, Find All Numbers Disappeared in an Array]
tags: [dsa, arrays, index-sign-marking, hashmap]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/Find All Numbers Dissappeared in Array 309e9c4cbab88009bff6ed9959918b0f.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Given `n` numbers each in `[1, n]`, return every value in that range that does not appear. A hash map of counts solves it in O(n) time and space, but the canonical trick encodes presence in the sign of `nums[value-1]`, achieving O(1) extra space.

## Approaches
- **Hash map of counts** — tally each number, then collect every `i` in `1..n` with a zero count. O(n) time, O(n) space.
- **In-place sign marking (optimal, added below)** — use each value as an index and negate the entry there to mark "this value is present"; positive entries afterward reveal the missing values. O(n) time, O(1) extra space.

## Best solution
The note's own solution (hash map):
```cpp
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        int size = nums.size();
        unordered_map<int, int> mp;
        vector<int> ans;

        for (auto number: nums) mp[number]++;

        for (int i = 1; i <= size; ++i) {
            if (mp[i] == 0) ans.push_back({i});
        }

        return ans;
    }
};
```

> [!note] Claude's addition
> **Canonical O(1)-space sign-marking solution.** For each value `v`, compute `idx = abs(v) - 1` and negate `nums[idx]` to mark that `v` is present. Use `abs()` when reading because a slot may already have been negated by an earlier value. After one pass, any index `i` whose `nums[i]` is still positive means `i+1` never appeared. This is the same idea as [[645 Set Mismatch]] and the [[Index Sign-Marking]] pattern.
>
> ```cpp
> class Solution {
> public:
>     vector<int> findDisappearedNumbers(vector<int>& nums) {
>         int n = nums.size();
>         for (int i = 0; i < n; ++i) {
>             int idx = abs(nums[i]) - 1;
>             if (nums[idx] > 0) nums[idx] = -nums[idx];
>         }
>         vector<int> ans;
>         for (int i = 0; i < n; ++i) {
>             if (nums[i] > 0) ans.push_back(i + 1);
>         }
>         return ans;
>     }
> };
> ```
> O(n) time, O(1) extra space (mutating the input in place).

## Notes
- The raw note only recorded the hash-map approach; the sign-marking approach above is the interview-preferred one for its O(1) space.

## Techniques
[[Index Sign-Marking]] · [[Hashmap Lookup Pattern]]

## Sources
- [[448 Find All Numbers Disappeared in an Array]] raw note — see `raw_path` above.
