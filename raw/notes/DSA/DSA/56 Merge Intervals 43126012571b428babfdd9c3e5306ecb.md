# 56. Merge Intervals

My approach:

Time Complexity: O(nlogn)

Space Complexity: O(n)

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