---
type: source
area: sde
title: 16 3Sum Closest
aliases: [16 3Sum Closest, 3Sum Closest]
tags: [dsa, arrays, two-pointer]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/16 3Sum Closest 10be9c4cbab880b582aeceeb3809e225.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Return the sum of three numbers closest to a target. Same skeleton as 3Sum — sort, fix one element, two-pointer the rest — but instead of matching an exact sum, track the running minimum absolute difference and remember the sum that produced it.

## Approaches
- **Sort + fix + two pointer** — sort ascending, loop `i`, then converge `j`/`k`. At each step compute `curr_sum` and `abs(target - curr_sum)`; keep the closest. Move `j`/`k` based on whether `curr_sum` is below or above target; short-circuit return on an exact hit. Time O(n²), space O(1).

## Best solution
```cpp
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        int size = nums.size();
        int min_diff = INT_MAX;
        int closest_sum = 0;

        sort(nums.begin(), nums.end());

        for (int i = 0; i < size - 2; ++i) {
            int j = i + 1, k = size - 1;
            while (j < k) {
                int curr_sum = nums[i] + nums[j] + nums[k];
                int diff = abs(target - curr_sum);

                if (diff < min_diff) {
                    min_diff = diff;
                    closest_sum = curr_sum;
                }

                if (curr_sum < target) j++;
                else if (curr_sum > target) k--;
                else return curr_sum;
            }
        }

        return closest_sum;
    }
};
```
Optimal because the sorted two-pointer pass makes the search O(n²) rather than the O(n³) of checking every triplet, while a single scalar tracks the best candidate.

## Notes
- No dedup logic is needed here — we want a sum, not a set of unique triplets, so duplicates don't hurt.
- The note calls out the loop bounds `size - 2` / `size - 1` and start `i + 1` so the very first iteration is a valid `[a, b, c]` and `closest_sum` isn't accidentally left at 0.
- An exact match (`curr_sum == target`) is the best possible answer, so return immediately.

## Techniques
[[k-Sum Pattern]] · [[Two Pointer Technique]]

## Sources
- [[16 3Sum Closest]] raw note — `raw/notes/DSA/DSA/16 3Sum Closest 10be9c4cbab880b582aeceeb3809e225.md`
