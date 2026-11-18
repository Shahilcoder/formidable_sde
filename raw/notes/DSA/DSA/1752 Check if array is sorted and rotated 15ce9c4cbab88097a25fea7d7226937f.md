# 1752. Check if array is sorted and rotated

Simple Traversal:

Time Complexity: O(N)

Space Complexity: O(1)

Well don’t care about rotated part, the testcases don’t check it. Only care about the sorted part.

Just traverse the array and look how many times `i`th element is greater than `i+1`th element, if this count is greater than 1 return false.

Else return true.

but make sure you let the algorithm check the last element with the first element as well.

so loop will run from `i=0` to `i=size` and compare `i` vs `(i+1) % size`.

Note: no need to do foolishly do circular runs of array again and again, because you already checked it dude, in the first run. Just compare the last and the first elment, and that’s the end of it.

SIMPLE AND EZ.

```cpp
class Solution {
public:
    bool check(vector<int>& nums) {
        int size = nums.size();

        int count = 0;

        for (int i=0; i<size; ++i) {
            if (nums[i] > nums[(i+1) % size]) count++;
            if (count > 1) return false;
        }

        return true;
    }
};
```