# 560. Subarray sum equals k

Prefix sum + Hash table approach:

Time Complexity: O(N) in best and average case

Space Complexity: O(N)

for each updated prefix sum s, find occurrences of s - k as prefix sum and add them to the count. You can store the occurrences into hash table so DON’T need to count again and again the occurrences.

NOTE: begin with prefix sum = 0, and add into hash table (0, 1) (very important)

Because if s = k itself, that means there is chance of no occurrence of s - k i.e 0, still the fact s = k appeared is our counted subarray.

```cpp
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int size = nums.size();
        unordered_map<int, int> mp;
        int count = 0, prefixSum = 0;
        mp[prefixSum] = 1;

        for (auto e: nums) {
            prefixSum += e;
            count += mp[prefixSum - k];
            mp[prefixSum]++;
        }

        return count;
    }
};
```