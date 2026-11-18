## Approach 1: Sorting + Hashmap + separate rank counter

- Time Complexity: O(nlog(n))
- Space Complexity: O(n)

```cpp
class Solution {
public:
    vector<int> arrayRankTransform(vector<int>& arr) {
        unordered_map<int, int> mp;
        vector<int> res = arr;
        int size = res.size();

        sort(res.begin(), res.end());

        // important: a separate rank counter
        int rank = 1;
        for (int i=0; i<size; ++i) {
            if (mp.find(res[i]) == mp.end())
                mp[res[i]] = rank++;
        }

        for (int i=0; i<size; ++i) res[i] = mp[arr[i]];

        return res;
    }
};
```

## **Approach 2: Sort Pairs (Value, Index) — No Hashmap**

- Time Complexity: O(nlog(n))
- Space Complexity: O(n)

```cpp
class Solution {
public:
    vector<int> arrayRankTransform(vector<int>& arr) {
        int n = arr.size();
        vector<pair<int,int>> pairs(n);
        for (int i = 0; i < n; i++)
            pairs[i] = {arr[i], i};

        sort(pairs.begin(), pairs.end());

        vector<int> res(n);
        int rank = 1;
        for (int i = 0; i < n; i++) {
            if (i > 0 && pairs[i].first != pairs[i-1].first)
                rank++;
            res[pairs[i].second] = rank;
        }
        return res;
    }
};
```

## **Approach 3: Sort + Unique + Binary Search**

- Time Complexity: O(nlog(n))
- Space Complexity: O(n)

```cpp
class Solution {
public:
    vector<int> arrayRankTransform(vector<int>& arr) {
        vector<int> sorted = arr;
        sort(sorted.begin(), sorted.end());

        // unique() doesn't erase elements.
        // It moves unique elements to the front and
        // returns an iterator to the new logical end.
        // 10 20 20 30 40 -> 10 20 30 40 ?? | ?? = garbage value
        sorted.erase(unique(sorted.begin(), sorted.end()), sorted.end());
        // Then sorted.erase() removes everything after the iterator.

        vector<int> res(arr.size());
        for (int i = 0; i < arr.size(); i++) {
		        // complicated, I don't understand this.
            int rank = lower_bound(sorted.begin(), sorted.end(), arr[i]) - sorted.begin() + 1;
            res[i] = rank;
        }

        return res;
    }
};
```

## **Approach 4: Ordered Map (std::map) — assign ranks via in-order traversal**

- Time Complexity: O(nlog(n))
- Space Complexity: O(n)

```cpp
class Solution {
public:
    vector<int> arrayRankTransform(vector<int>& arr) {
        map<int,int> mp; // keys auto-sorted (BST under the hood)
        for (int x : arr) mp[x] = 0;

        // important: single in-order pass assigns ranks directly
        int rank = 1;
        for (auto& [key, val] : mp)
            val = rank++;

        vector<int> res;
        for (int x : arr)
            res.push_back(mp[x]);
        return res;
    }
};
```

## Comparison:

- Approach 1 (unordered_map) is fastest in practice due to O(1) average lookups but has no ordering guarantee during insertion
- Approach 2 avoids the hashmap entirely by carrying the original index through the sort
- Approach 3 trades a hashmap for binary search, which is handy if you want to keep the "unique sorted values" array around for other queries
- Approach 4 is the most concise since sorting and de-duplication happen implicitly as part of building the map, but constant factors are worse than unordered_map due to the underlying red-black tree.