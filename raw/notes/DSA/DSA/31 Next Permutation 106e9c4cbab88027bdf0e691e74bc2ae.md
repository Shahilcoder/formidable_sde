# 31. Next Permutation

Linear Approach:

Time Complexity: O(3n) → O(n)

Space Complexity: O (1)

Find the point where the value dips, i.e. becomes small when traversing from backside

if 

there is no dip point, then that means it's the largest permutation, reverse the array

else

find the next larger element traversing from back, then swap the dip point and that element now reverse all the elements after dip point, to make sure they are minimum

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int size = nums.size();
        int index = -1;

        // find the dip from back, from n-2
        for (int i=size-2; i>=0; --i) {
            if (nums[i] < nums[i+1]) {
                index = i;
                break;
            }
        }

        // if didn't find any dip, that means its largest permutation
        if (index == -1) {
            reverse(nums.begin(), nums.end());
            return;
        }

        // search from back (n-1) again the element just greater than dip
        for (int i=size-1; i>index; --i) {
            if (nums[i] > nums[index]) {
                swap(nums[i], nums[index]);
                break;
            }
        }

        // reverse the rest of array after the dip point to keep it minimum value
        reverse(nums.begin() + index + 1, nums.end());
    }
};
```