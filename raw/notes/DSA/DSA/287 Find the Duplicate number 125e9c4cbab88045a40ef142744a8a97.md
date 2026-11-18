# 287. Find the Duplicate number

Linked list’s cycle detection and Floyd’s algorithm:

Time Complexity: O(n)

Space Complexity: O(1)

Watch Neetcode’s video on this topic

```cpp
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int slow = 0, fast = 0;

        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (slow != fast);

        int slow2 = 0;
        while (slow != slow2) {
            slow = nums[slow];
            slow2 = nums[slow2];
        }

        return slow;
    }
};
```