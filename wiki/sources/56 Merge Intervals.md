---
type: source
area: sde
title: 56 Merge Intervals
aliases: [56 Merge Intervals, Merge Intervals]
tags: [dsa, arrays, greedy]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/56 Merge Intervals 43126012571b428babfdd9c3e5306ecb.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Given a collection of intervals, merge all overlapping ones. The winning idea: sort by start, then sweep once — greedily extend the last interval in the result whenever the next interval starts before that interval ends.

## Approaches
- **Sort + greedy sweep (O(n log n) time, O(n) space):** sort intervals by their start value, seed the result with the first interval, then for each subsequent interval either merge it into the last result interval (overlap) or append it (no overlap).

## Best solution
```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        int size = intervals.size();

        sort(intervals.begin(), intervals.end(), [](vector<int> &a, vector<int> &b) {
            return a[0] < b[0];
        });

        vector<vector<int>> res;
        res.push_back(intervals[0]);

        int i = 1;

        while (i < size) {
            vector<int> &last = res.back();

            if (intervals[i][0] <= last[1]) {
                // can do this with ternary operator as well, saves space
                last[0] = min(last[0], intervals[i][0]);
                last[1] = max(last[1], intervals[i][1]);
            } else {
                res.push_back(intervals[i]);
            }

            i++;
        }

        return res;
    }
};
```
Optimal because sorting by start guarantees any overlap is with the immediately preceding interval, so a single linear pass merges everything; cost is dominated by the O(n log n) sort.

## Notes
The `vector<int> &last = res.back();` reference is the crux — it lets the merge mutate the interval already sitting in the result in place. Sorting by start is what makes "check only against the last result interval" correct; without the sort you'd have to compare against all previous intervals.

## Techniques
[[Greedy Algorithm]]

## Sources
- [[56 Merge Intervals]] raw note — `raw/notes/DSA/DSA/56 Merge Intervals 43126012571b428babfdd9c3e5306ecb.md`
