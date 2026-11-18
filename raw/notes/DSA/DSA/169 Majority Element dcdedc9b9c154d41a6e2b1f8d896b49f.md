# 169. Majority Element

Map (loosely hashtable) solution:

Time Complexity: O(n)

Space Complexity: O(n)

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int threshold = nums.size() / 2;
        int majority = 0;
        unordered_map<int, int> map;

        for (auto e: nums) {
            if (map.find(e) == map.end()) map[e] = 1;
            else map[e]++;

            if (map[e] > threshold) {
                majority = e;
                break;
            }
        }

        return majority;
    }
};
```

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int threshold = nums.size() / 2;
        unordered_map<int, int> map;

        for (auto e: nums) {
		        // map[e] will by default keep 0, for new keys, so this code will lead to ++ to 1
		        // for new keys
            map[e]++;
            if (map[e] > threshold) return e;
        }

        return -1;
    }
};
```

Sort and take (n / 2)th element:

Time Complexity: O(nlogn)

Space Complexity: O(1)

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        sort(nums.begin(), nums.end());

        return nums[nums.size() / 2];
    }
};
```

Voting strategy (Moore’s algorithm):

This code makes sense, and is according to video explanation.

Time Complexity: O(n)

Space Complexity: O(1)

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int size = nums.size();
        int candidate = nums[0];
        int vote = 1;

        for (int i=1; i < size; ++i) {
            if (candidate == nums[i]) vote++;
            else vote--;

            if (vote == 0) {
                candidate = nums[i];
                vote++;
            }
        }

        return candidate;
    }
};
```