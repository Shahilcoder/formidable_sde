# 1480. Running Sum of 1d Array

My solution:

```cpp
class Solution {
public:
    vector<int> runningSum(vector<int>& nums) {
        int accumulator = 0;
        int size = nums.size();

        for (int i=0; i < size; ++i) {
            int temp = nums[i];
            nums[i] += accumulator;
            accumulator += temp;
        }

        return nums;
    }
};
```

Efficient and better:

```cpp
class Solution {
public:
    vector<int> runningSum(vector<int>& nums) {
        int size = nums.size();
        int i = 1;

        while (i < size) {
            nums[i] += nums[i-1];
            ++i;
        }

        return nums;
    }
};
```