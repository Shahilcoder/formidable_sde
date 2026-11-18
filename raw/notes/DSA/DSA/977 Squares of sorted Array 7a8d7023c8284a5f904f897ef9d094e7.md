# 977. Squares of sorted Array

Smart two pointer approach:

Now, we can have two pointers `l` to left most element, `r` to most right element.

Create `res` result array same size as `A`.

Move from right to left in `res` and past `max(abs(A[l]), abs(A[r]))`, move correspondingly `l++` or `r--`.

Time Complexity: O(n)

Space Complexity: O(n)

```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        int size = nums.size();
        int s=0, e=size-1, k=size-1;
        int square;

        vector<int> res(size);

        while (k >= 0) {
            if (abs(nums[s]) < abs(nums[e])) {
                square = nums[e];
                e--;
            }
            else {
                square = nums[s];
                s++;
            }

            res[k--] = square * square;
        }

        return res;
    }
};
```

Shorter version:

```cpp
class Solution {
public:
    int square(int a) {
        return a*a;
    }

    vector<int> sortedSquares(vector<int>& nums) {
        int size = nums.size();
        vector<int> res(size);

        int l=0, r=size-1, k=size-1;

        while (k >= 0) {
            if (abs(nums[l]) > abs(nums[r])) res[k--] = square(nums[l++]);
            else res[k--] = square(nums[r--]);
        }

        return res;
    }
};
```