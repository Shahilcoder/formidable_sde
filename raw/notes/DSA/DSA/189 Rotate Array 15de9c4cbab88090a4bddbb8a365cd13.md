# 189. Rotate Array

Straight way:

Time Complexity: O(n)

Space Complexity: O(n)

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int size = nums.size();
        vector<int> result(size);

        for (int i=0; i<size; ++i) {
            result[(i+k) % size] = nums[i];
        }

        nums = result;
    }
};
```

Queue Approach:

Time Complexity: O(n)

Space Complexity: O(n)

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int size = nums.size();
        queue<int> q;

        int i = 0;
        int temp = k;
        while (temp > 0) {
            q.push(nums[(i+k) % size]);
            nums[(i+k) % size] = nums[i];
            i++;
            temp--;
        }

        temp = size - k;
        while (temp > 0) {
            q.push(nums[(i+k) % size]);
            nums[(i+k) % size] = q.front();
            q.pop();
            i++;
            temp--;
        }
    }
};
```

Reverse Reverse:

Time Complexity: O(n)

Space Complexity: O(1)

Watch Neetcode. (Videos are quick)

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int size = nums.size();
        // k can be greater than or equal to size of the array
        // rather than useless rotations, chop it off to useful rotations
        k = k % size;

        reverse(nums.begin(), nums.end());
        reverse(nums.begin(), nums.begin() + k);
        reverse(nums.begin() + k, nums.end());
    }
};
```