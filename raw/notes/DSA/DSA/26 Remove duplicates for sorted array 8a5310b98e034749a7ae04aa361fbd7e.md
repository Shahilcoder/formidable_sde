# 26. Remove duplicates for sorted array

My Two pointer approach:

Time Complexity: O(n)

Space Complexity: O(1)

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int size = nums.size();

        int slow = 1;
        int fast = 1;

        while (fast < size) {
            if (nums[fast-1] != nums[fast]) {
                nums[slow++] = nums[fast];
            }

            fast++;
        }

        return slow;
    }
};
```