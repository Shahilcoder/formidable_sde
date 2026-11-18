## Approach 1: increase digits + sorting

**Time complexity: O(1)**

_The total count of sequential-digit numbers (2+ digits, digits 1-9) is fixed — there are only 8 two-digit ones, 7 three-digit, down to 1 nine-digit, 36 total, regardless of low/high. So the while loop runs a bounded, constant number of iterations, and the final sort is over at most 36 elements — also constant._

**Space complexity: O(1)**

_beyond the output — `result` holds at most 36 numbers, a constant bound, so it doesn't grow with input size._

```cpp
class Solution {
public:
    vector<int> sequentialDigits(int low, int high) {
        vector<int> result;

        int d = 1;
        int starting = d;
        int num = d;

        while (starting <= 9) {
            if (num >= low && num <= high) result.push_back(num);

            d++;
            num = num * 10 + d;

            if (num > high || d > 9) {
                d = ++starting;
                num = d;
            }
        }

        sort(result.begin(), result.end());

        return result;
    }
};
```

## Approach 2: substring generation (cleanest)

**Time Complexity: O(1)**

**Space Complexity: O(1)**

```cpp
class Solution {
public:
    vector<int> sequentialDigits(int low, int high) {
        string s = "123456789";
        vector<int> result;

        for (int len = 2; len <= 9; len++) {
            for (int i = 0; i + len <= 9; i++) {
                int num = stoi(s.substr(i, len));
                if (num >= low && num <= high)
                    result.push_back(num);
            }
        }

        // no sort() call -- numbers are generated in increasing order already:
        // shorter lengths come first, and within a length, starting digit increases.
        return result;
    }
};
```
