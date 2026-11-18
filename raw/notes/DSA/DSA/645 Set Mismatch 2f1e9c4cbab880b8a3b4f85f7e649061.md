# 645. Set Mismatch

**1st Approach: My trial, Find Sum   &   Sum of squares of n numbers.**

Time Complexity: O(n)

Space Complexity: O(1)

[https://youtu.be/d-ulaeRBA64?si=N-F8Y9kB0jmsXmi9&t=732](https://youtu.be/d-ulaeRBA64?si=N-F8Y9kB0jmsXmi9&t=732)

```cpp
class Solution {
public:
    vector<int> findErrorNums(vector<int>& nums) {
        long size = nums.size();

        long sum1 = size * (size + 1) / 2;
        long sqrSum1 = size * (size + 1) * (2 * size + 1) / 6;

        long sum2 = 0;
        long sqrSum2 = 0;

        for (long number: nums) {
            sum2 += number;
            sqrSum2 += number * number;
        }

        int x = sum2 - sum1;
        int y = sqrSum2 - sqrSum1;
	
				// d - m = sum2 - sum1 = x
				// d^2 - m^2 = sqrSum2 - sqrSum1 = y

				// So,
				// d - m = x -> (i)
				// d^2 - m^2 = y OR (d - m)(d + m) = y

				// Therefore,
				// d + m = y / x -> (ii)
				// add (i) and (ii) equations together:
        int duplicate = (y + x * x) / (2 * x);
        
        // And from (i),
        int missing = duplicate - x;

        return {duplicate, missing};
    }
};
```

**2nd Approach: Hashmap + traversal from 1 to n**

Time Complexity: O(n)

Space Complexity: O(n)

```cpp
class Solution {
public:
    vector<int> findErrorNums(vector<int>& nums) {
        int size = nums.size();
        vector<int> ans(2);
        unordered_map<int, int> mp;

        for (auto number: nums) mp[number]++;

				// by default whenever you try to access/index by a key
				// in an unordered_map it stores the value as 0
				// for that key, when no such {key, value} pair exists
        for (int i=1; i<=size; ++i) {
            if (mp[i] == 2) ans[0] = i;
            else if (mp[i] == 0) ans[1] = i;
        }

        return ans;
    }
};
```

**3rd Approach: Negation trick**

Time Complexity: O(n)

Space Complexity: O(1)

[https://youtu.be/d-ulaeRBA64?si=Znu-aqlBj4v1cWrk&t=293](https://youtu.be/d-ulaeRBA64?si=Znu-aqlBj4v1cWrk&t=293)

I have simplified the code though. Mine is more intuitive.

```cpp
class Solution {
public:
    vector<int> findErrorNums(vector<int>& nums) {
        int size = nums.size();
        vector<int> ans(2);

				// Take the values in the array as index (number - 1). and negate.
        for (auto number: nums) {
            int p_number = abs(number);
            
            // if the value was already negated, that means
            // its due to duplication.
            if (nums[p_number - 1] < 0) {
                ans[0] = p_number;
                continue; // Skip the negation part below, that will make value positive again.
            }

            nums[p_number - 1] = -nums[p_number - 1];
        }

				// now loop 1 to n
        for (int i=1; i <= size; ++i) {
		        // the missing number when used as index (number - 1)
		        // will have positive number there.
            if (nums[i-1] >= 0) {
                ans[1] = i;
                break;
            }
        }

        return ans;
    }
};
```