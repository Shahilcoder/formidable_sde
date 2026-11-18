# 1470. Shuffle the array

**1st Approach:**

Time Complexity: O(n)

Space Complexity: O(n)

```cpp
class Solution {
public:
    vector<int> shuffle(vector<int>& nums, int n) {
        vector<int> result;
        int i = 0;

        while (i < n) {
            result.push_back(nums[i]);
            result.push_back(nums[i+n]);
            i++;
        }

        return result;
    }
};
```

OR:

```cpp
class Solution {
public:
    vector<int> shuffle(vector<int>& nums, int n) {
        vector<int> result(2 * n);
        int i = 0, first = 0;
        int second = n;

        while (first < n) {
            result[i++] = nums[first++];
            result[i++] = nums[second++];
        }

        return result;
    }
};
```

**2nd Approach:** Bit manipulation trick

Time Complexity: O(n)

Space Complexity: O(1)

[https://www.youtube.com/watch?v=IvIKD_EU8BY](https://www.youtube.com/watch?v=IvIKD_EU8BY)

```cpp
class Solution {
public:
    vector<int> shuffle(vector<int>& nums, int n) {
        for (int i=0; i<n; ++i) {
            // x
            nums[i] = nums[i] << 10;

            int y = nums[n + i];
            nums[i] = nums[i] | y;
        }

        int last = 2*n - 1;
        for (int j=n-1; j>=0; --j) {
            int y = nums[j] & 1023;
            int x = nums[j] >> 10;

            nums[last--] = y;
            nums[last--] = x;
        }

        // at the end it is guaranteed, that last == -1;

        return nums;
    }
};
```