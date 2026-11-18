---
type: source
area: sde
title: 645 Set Mismatch
aliases: [645 Set Mismatch, Set Mismatch]
tags: [dsa, arrays, index-sign-marking, hashmap, math]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/645 Set Mismatch 2f1e9c4cbab880b8a3b4f85f7e649061.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
An array should hold `1..n` but one number is duplicated and another is missing; return both. The optimal, space-free approach is the sign-marking trick: use each value as an index and negate the entry there — the value that finds its slot already negative is the duplicate, and the slot left positive gives the missing value.

## Approaches
- **Sum + sum-of-squares (math)** — from `d - m = sum2 - sum1` and `d^2 - m^2 = sqrSum2 - sqrSum1`, solve the two equations for duplicate `d` and missing `m`. O(n) time, O(1) space; watch integer overflow (uses `long`).
- **Hash map of counts** — tally counts, then scan `1..n`: the value with count 2 is the duplicate, count 0 is the missing. O(n) time, O(n) space.
- **Negation / index sign-marking (optimal)** — negate `nums[abs(v)-1]` for each value; a slot already negative flags the duplicate, and the one still positive after the pass gives the missing number. O(n) time, O(1) space.

## Best solution
```cpp
class Solution {
public:
    vector<int> findErrorNums(vector<int>& nums) {
        int size = nums.size();
        vector<int> ans(2);

        // treat each value as index (number - 1) and negate
        for (auto number: nums) {
            int p_number = abs(number);

            // if already negated, it's due to duplication
            if (nums[p_number - 1] < 0) {
                ans[0] = p_number;
                continue; // skip negating back to positive
            }

            nums[p_number - 1] = -nums[p_number - 1];
        }

        // the missing number's slot stays positive
        for (int i = 1; i <= size; ++i) {
            if (nums[i - 1] >= 0) {
                ans[1] = i;
                break;
            }
        }

        return ans;
    }
};
```
Optimal: O(n) time and O(1) extra space, and unlike the math approach it has no overflow subtlety.

## Notes
- Same core idea as [[448 Find All Numbers Disappeared in an Array]] — encode presence in the sign of the value at index `v-1`.
- The math approach is elegant but needs `long` to avoid overflow on the squared sums.

## Techniques
[[Index Sign-Marking]] · [[Hashmap Lookup Pattern]]

## Sources
- [[645 Set Mismatch]] raw note — see `raw_path` above.
