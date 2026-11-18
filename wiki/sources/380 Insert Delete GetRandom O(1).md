---
type: source
area: sde
title: 380 Insert Delete GetRandom O(1)
aliases: [380 Insert Delete GetRandom O(1), Insert Delete GetRandom O(1)]
tags: [dsa, arrays, hashmap]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/380 Insert Delete get random o1 f40fcf7096eb441ab760e78cede92ce0.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Design a set supporting `insert`, `remove`, and `getRandom`, all in average O(1). The trick is pairing a dynamic array (for O(1) uniform random access) with a hash map from value to its index (for O(1) lookup); removal swaps the target with the last element so the array stays gap-free.

## Approaches
- **Array + hash map (optimal)** — the `vector` holds the elements so `getRandom` is `nums[rand() % size]`; `mp` maps value → index for O(1) `insert`/`remove` membership checks. To remove, overwrite the target slot with the last element, fix that element's index in the map, then `pop_back`. All operations average O(1); O(n) space.

## Best solution
```cpp
class RandomizedSet {
private:
    unordered_map<int, int> mp;
    vector<int> nums;
public:
    RandomizedSet() {}

    bool insert(int val) {
        if (mp.find(val) != mp.end()) return false;
        nums.push_back(val);
        mp[val] = nums.size() - 1;
        return true;
    }

    bool remove(int val) {
        if (mp.find(val) == mp.end()) return false;
        // move the last element into val's slot, then pop the tail
        int last = nums.back();
        nums[mp[val]] = last;
        nums.pop_back();
        // update the moved element's recorded index, then drop val
        mp[last] = mp[val];
        mp.erase(val);
        return true;
    }

    int getRandom() {
        return nums[rand() % nums.size()];
    }
};
```
Optimal: the swap-with-last removal avoids shifting the array (which would be O(n)), keeping every operation average O(1).

## Notes
- Order in `remove` matters: fix `mp[last]` before `mp.erase(val)`; when `val` is the last element the two lines are self-consistent.

## Techniques
[[Hashmap Lookup Pattern]]

## Sources
- [[380 Insert Delete GetRandom O(1)]] raw note — see `raw_path` above.
