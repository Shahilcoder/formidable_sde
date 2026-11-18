# 16. 3Sum Closest

Sorting, for loop and Two pointer approach:

Time Complexity: O(n^2)

Space Complexity: O(1)

Sort the array, Loop through take one element linearly, and for next upcoming elements, do two pointer approach at them see if the difference between target and the sum of three selected elements is getting lower, at end either the sum = target return that, or loop will run out and just return that sum.

```cpp
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        int size = nums.size();
        int min_diff = INT_MAX;

        int closest_sum = 0;

        sort(nums.begin(), nums.end());

        // notice the size - 2, size - 1, and i + 1
        // loop will execute successfully once for [a, b, c]
        // so that sum = a + b + c and not sum = 0 by default
        for (int i=0; i < size-2; ++i) {
            int j = i+1, k = size-1;
            while (j < k) {
                int curr_sum = nums[i] + nums[j] + nums[k];
                int diff = abs(target - curr_sum);

                if (diff < min_diff) {
                    min_diff = diff;
                    closest_sum = curr_sum;
                }

                if (curr_sum < target) j++;
                else if (curr_sum > target) k--;
                // curr_sum == target
                else return curr_sum;
            }
        }

        return closest_sum;
    }
};
```