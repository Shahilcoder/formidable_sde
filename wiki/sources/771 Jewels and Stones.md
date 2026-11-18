---
type: source
area: sde
title: 771 Jewels and Stones
aliases: [771 Jewels and Stones, Jewels and Stones]
tags: [dsa, string, hashmap]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/771 Jewels and Stones 29ae9c4cbab880cfbafbfadf875b88fe.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Count how many characters in `stones` are also jewel types listed in `jewels`. Load the jewel characters into an `unordered_set` (or a boolean array) for O(1) membership, then scan the stones once.

## Approaches
- **`unordered_set` (optimal / cleanest)** — build a set from `jewels`, count stones whose character is in the set. O(|J| + |S|) time, O(|J|) space.
- **`unordered_map`** — same idea using a map with dummy values; works but wastes memory storing counts you don't need. O(|J| + |S|) time, O(|J|) space.
- **Brute force** — for each stone scan all jewels. O(|J| * |S|) time, O(1) space.
- **Boolean array (fastest in practice)** — a 128-entry `vector<bool>` indexed by char; constant-time lookups, no hashing overhead. O(|J| + |S|) time, O(1) space (fixed 128).

## Best solution
```cpp
int numJewelsInStones(string jewels, string stones) {
    unordered_set<char> jewelSet(jewels.begin(), jewels.end());
    int count = 0;
    for (char stone : stones)
        if (jewelSet.count(stone)) count++;
    return count;
}
```
Optimal: linear time with O(1) average-case lookups; a set is semantically cleaner than a map since only membership matters.

## Notes
- If inputs are guaranteed ASCII, the 128-entry boolean array is fastest in practice (no hashing), at fixed constant space.

## Techniques
[[Hashmap Lookup Pattern]]

## Sources
- [[771 Jewels and Stones]] raw note — see `raw_path` above.
