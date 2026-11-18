# 1010. Pairs of Songs

Hash table storing remainders occurrence:

Time complexity: O(n)

Space complexity: O(n)

Logic hai `t % 60` karo, if divisible nhi hai toh kitna aur chahiye divisible hone ke liye?? `60 - t % 60`  check aisa number OR greater number jiska remainder hi yeh value ho wo exists karta hai ki nhi?? because chahe us number `60 - t % 60` ko add karo ya greater number wale ko jiska remainder hi `60 - t % 60` ho, both will ALWAYS make it divisible.

Example:

20 % 60 = 20, yani 40 more chahiye

now the number 40 itself bhi chalega, and 100 for which 100 % 60 = 40 BHI chalega, as dono ko 20 se add karoge toh 60 se divisible ho jayega biru.

---

Take `pairs` count 0.

You check if for each `t` in `time`  if its undivisible by 60, how much more does it need to be divisible by 60? that is `60 - (t % 60)` . Check does that remainder exists in hashtable or not, just add the occurrences into `pairs` . Then also make sure to update `t % 60` occurrence into hashtable.

if `t` is divisible by 60, check if remainder `0` key exists in hashtable or not, because you need atleast one more to make a pair right? add that to `pairs` . Also update `0` or `t % 60` remainder occurrence in hashtable.

```cpp
class Solution {
public:
    int numPairsDivisibleBy60(vector<int>& time) {
        int size = time.size();
        unordered_map<int, int> mp;
        int pairs = 0;

        for (auto t: time) {
            if (t % 60 != 0) {
                int key = 60 - (t % 60);
                pairs += mp[key];

            } else pairs += mp[0];

            mp[t % 60]++;
        }

        return pairs;
    }
};
```

Vector Approach:

Time complexity: O(n)

Space complexity: O(n)

Though used more space for literally all indexes from 0 to 59, (60 indexes, each index denotes the remainder value) but vector is much faster as you just directly access the value at index, knowing you will never index out of bound…

While a traditional hashtable you need to search if the key exists in the hashtable or not, which is though O(1) you still compute the hashing function, slower than direct vector index access.

```cpp
class Solution {
public:
    int numPairsDivisibleBy60(vector<int>& time) {
        int size = time.size();
        vector<int> remainders(60, 0);
        int pairs = 0;

        for (auto t: time) {
            if (t % 60 != 0) {
                int index = 60 - (t % 60);
                pairs += remainders[index];

            } else pairs += remainders[0];

            remainders[t % 60]++;
        }

        return pairs;
    }
};
```