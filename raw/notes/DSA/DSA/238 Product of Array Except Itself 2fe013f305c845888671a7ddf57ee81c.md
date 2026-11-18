# 238. Product of Array Except Itself

Modified prefix and then suffix product approach:

Time Complexity: O(n)

Space Complexity: O(n)

Taking p = 1, multiplying it with the array element, then p *= nums[i], then move ahead i++ and repeat. Then do same for p = 1 from backwards..

Type 1: Two separate loops

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int size = nums.size();
        int p = 1;

        vector<int> res(size, 0);

        for (int i=0; i<size; ++i) {
            res[i] = p;
            p *= nums[i];
        }

        p = 1;
        for (int i=size-1; i>=0; --i) {
            res[i] *= p;
            p *= nums[i];
        }

        return res;
    }
};
```

Type 2: All in one loop

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int size = nums.size();
        int p1 = 1, p2 = 1;

        vector<int> res(size, 1);

        for (int i=0; i<size; ++i) {
            res[i] *= p1;
            p1 *= nums[i];

            int j=size-1-i;
            res[j] *= p2;
            p2 *= nums[j];
        }

        return res;
    }
};
```