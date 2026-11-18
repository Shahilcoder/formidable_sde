# 88. Merge sorted array

Direct solution just write nums2 at end of nums1, then sort using introspective sort by C++:

Time complexity: O(nlogn)

Space complexity: O(1)

```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        for (int i=0; i < n; ++i) {
            nums1[m + i] = nums2[i];
        }

        sort(nums1.begin(), nums1.end());
    }
};
```

Second solution is to use the **merge strategy we do in merge sort algorithm**, BUT IN REVERSE, so that largest elements are overwritten from back and no risk of losing the original nums1 values during execution.

Time complexity: O(Max(m, n))

Space complexity: O(1)

```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i = m - 1, j = n - 1, k = m + n - 1;

        while (i >= 0 && j >= 0) {
            if (nums1[i] >= nums2[j]) nums1[k--] = nums1[i--];
            else nums1[k--] = nums2[j--];
        }

        while (i >= 0) nums1[k--] = nums1[i--];
        while (j >= 0) nums1[k--] = nums2[j--];
    }
};
```