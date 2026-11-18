# 3289. The Two Sneaky Numbers of Digitville

**First Approach:**

Sorting and two pointers (slow and fast)

Time Complexity: O(n log(n))

Space Complexity: O(1)

```cpp
class Solution {
public:
    vector<int> getSneakyNumbers(vector<int>& nums) {
        vector<int> answer;
        int size = nums.size();

        // O(nlog(n))
        sort(nums.begin(), nums.end());

        int slow = 0;
        int fast = 1;

        while (fast < size) {
            if (nums[slow] == nums[fast]) answer.push_back(nums[fast]);

            slow++;
            fast++;
        }

        return answer;
    }
};
```

**Second Approach:**

Fill the set, while detecting if there is extra element being inserted?

Time Complexity: O(n) [set.count() is constant on average case]

Space Complexity: O(n)

```cpp
class Solution {
public:
    vector<int> getSneakyNumbers(vector<int>& nums) {
        vector<int> answer;
        unordered_set<int> s;
        
        for (auto num: nums) {
            if (s.count(num)) answer.push_back(num);
            else s.insert(num);
        }

        return answer;
    }
};
```