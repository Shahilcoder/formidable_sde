---
type: source
area: sde
title: 1010 Pairs of Songs With Total Durations Divisible by 60
aliases: [1010 Pairs of Songs With Total Durations Divisible by 60, Pairs of Songs With Total Durations Divisible by 60]
tags: [dsa, arrays, hashmap]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/1010 Pairs of Songs 10ce9c4cbab88030bb67f1c9cd101568.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Count pairs `(i, j)` whose durations sum to a multiple of 60. The winning idea is a single pass that keeps a frequency table of remainders mod 60: for each song with remainder `r`, the complement remainder that completes a multiple of 60 is `(60 - r) % 60`, so add the count of complements already seen before recording the current remainder.

## Approaches
- **Hash table of remainders** — `unordered_map<int,int>` mapping remainder → count seen so far. For each `t`, if `t % 60 != 0` look up key `60 - (t % 60)`, else look up key `0`; add that count to `pairs`, then increment `mp[t % 60]`. O(n) time, O(n) space (bounded by 60 keys).
- **Fixed-size vector of remainders** — same logic but a `vector<int> remainders(60)` instead of a hashmap. O(n) time, O(n) space. Faster in practice: direct index access avoids computing the hash function, and indexing is guaranteed in-bounds.

## Best solution
```cpp
class Solution {
public:
    int numPairsDivisibleBy60(vector<int>& time) {
        vector<int> remainders(60, 0);
        int pairs = 0;

        for (auto t : time) {
            if (t % 60 != 0) {
                int index = 60 - (t % 60);
                pairs += remainders[index];
            } else {
                pairs += remainders[0];
            }
            remainders[t % 60]++;
        }

        return pairs;
    }
};
```
Optimal because it is a single O(n) pass with O(1) extra space (only 60 buckets), and the fixed-size vector beats the hashmap by skipping hashing entirely while never risking an out-of-bounds access.

## Notes
- Key insight: any number whose remainder equals `60 - (t % 60)` completes the pair — not just that exact number. E.g. `20 % 60 = 20` needs 40 more; both `40` and `100` (`100 % 60 = 40`) work.
- Add complement counts BEFORE recording the current remainder, so a song is never paired with itself.
- The `t % 60 == 0` case pairs with other multiples of 60 (remainder 0), so it needs the `remainders[0]` count explicitly rather than key `60`.

## Techniques
[[Hashmap Lookup Pattern]]

## Sources
- [[1010 Pairs of Songs With Total Durations Divisible by 60]] raw note — `raw/notes/DSA/DSA/1010 Pairs of Songs 10ce9c4cbab88030bb67f1c9cd101568.md`
