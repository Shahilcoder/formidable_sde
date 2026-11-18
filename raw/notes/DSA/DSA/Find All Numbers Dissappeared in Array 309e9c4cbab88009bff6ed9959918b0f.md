# Find All Numbers Dissappeared in Array

**1st Approach: Hash map**

Time Complexity: O(n)

Space Complexity: O(n)    or    O(n - k) where k → count of missing numbers

```cpp
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        int size = nums.size();
        unordered_map<int, int> mp;
        vector<int> ans;

        for (auto number: nums) mp[number]++;

        for (int i=1; i<=size; ++i) {
            if (mp[i] == 0) ans.push_back({i});
        }

        return ans;
    }
};
```