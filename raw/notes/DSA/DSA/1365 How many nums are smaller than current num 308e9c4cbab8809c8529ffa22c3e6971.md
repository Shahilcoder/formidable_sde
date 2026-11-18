# 1365.  How many nums are smaller than current num

**1st Approach: Brute force**

Time Complexity: O(n^2)

Space Complexity: O(n)

```cpp
class Solution {
    public int[] smallerNumbersThanCurrent(int[] nums) {
        int n=nums.length;
        int ans[] = new int[n];
        for(int i=0;i<n;i++){
            int count=0;
            for(int j=0;j<n;j++){
                if(nums[i]>nums[j]){
                    count++;
                }
                ans[i] = count;;
            }
        }
        return ans;
    }
};
```

**2nd Approach: Hash map**

Time Complexity: O(nlogn)

Space Complexity: O(n)

```cpp
class Solution {
public:
    vector<int> smallerNumbersThanCurrent(vector<int>& nums) {
        int size = nums.size();
        vector<int> copy = nums;
        unordered_map<int, int> mp;
				
				// Sort, and the index will now denote count of numbers smaller
				// than a particular value at that index.
        sort(copy.begin(), copy.end());

        for (int i=0; i<size; ++i) {
		        // Do this so that duplicates don't overwrite the original
		        // correct answer about count of smaller numbers
		        // for the value at that index.
            if (mp.find(copy[i]) == mp.end()) mp[copy[i]] = i;
        }

        for (int i=0; i<size; ++i) {
            nums[i] = mp[nums[i]];
        }

        return nums;
    }
};
```

**3rd Approach: Tally array with prefix Sum**

Time Complexity: O(n)

Space Complexity: O(1) [ONLY Because editing the same input array]

[https://youtu.be/eHqwoWiMDfY?si=dqN6USEkWBu6cRwG](https://youtu.be/eHqwoWiMDfY?si=dqN6USEkWBu6cRwG)

```cpp
class Solution {
public:
    vector<int> smallerNumbersThanCurrent(vector<int>& nums) {
        int size = nums.size();
        vector<int> tallyWithPrefixSum(101);

        for (auto number: nums) tallyWithPrefixSum[number]++;

        for (int i=1; i<101; ++i) tallyWithPrefixSum[i] += tallyWithPrefixSum[i-1];

        for (int i=0; i<size; ++i) {
            int position = nums[i];

            if (position == 0) nums[i] = 0;
            else nums[i] = tallyWithPrefixSum[position - 1];
        }

        return nums;
    }
};
```