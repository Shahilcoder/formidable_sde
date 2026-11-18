---
type: pattern
area: sde
title: Hashmap Lookup Pattern
aliases: [Hashmap Lookup Pattern, Index by Key, Array to Map]
tags: [dsa, web-dev, hashmap, performance, complexity]
status: draft
source_count: 11
created: 2026-07-12
updated: 2026-07-12
---

## Summary
When you repeatedly need to find items in an array by some key, **build a lookup map once** (`{key → item}`) and index into it in O(1), instead of calling `find()` on every access — which is O(n) each time and O(n·m) over m lookups.

## Details
Naïve version — `find()` inside a loop is quadratic:
```js
// O(n * m): for each pet, scan all parents
for (let pet of pets) {
  pet.parentName = parents.find(p => p.id === pet.parentId).name;
}
```

Hashmap version — pay O(n) to build the index, then each lookup is O(1):
```js
// O(n + m): index parents by id once, then O(1) per pet
const map = {};
for (let obj of parents) {
  map[obj.id] = obj;
}
for (let pet of pets) {
  pet.parentName = map[pet.parentId].name;
}
```

**When to use:** any "join two lists on a key" situation — enriching API results, resolving foreign-key-like references on the client, deduping, counting occurrences. This is the single most common place web code accidentally goes quadratic.

**Notes:** a plain object works for string/number keys; use a real `Map` when keys are objects or when insertion order / non-string keys matter. Guard against missing keys (`map[id]?.name`) so a lookup miss doesn't throw.

## DSA usage
The same "trade O(n) space for O(1) lookups" idea is the workhorse of array/string interview problems. Three recurring shapes:

**1. Complement counting** — while scanning, ask the map whether the *complement* you need has already been seen, so you find a pair in one pass instead of a nested loop.
```cpp
// Two Sum: for each x, has (target - x) been seen?
unordered_map<int,int> seen;                 // value -> index
for (int i = 0; i < nums.size(); ++i) {
    int need = target - nums[i];
    if (seen.count(need)) return {seen[need], i};
    seen[nums[i]] = i;
}
```
This generalizes: prefix-sum + hashmap counts subarrays summing to `k` (store how many times each running sum appeared, look up `sum - k`); pairing durations by `(a + b) % 60 == 0` looks up the complementary remainder.

**2. Frequency counting** — `map[x]++` turns "how often / does it exist" questions into O(1) queries: tallying occurrences to find a majority, building a set of "which characters are jewels," counting how many values are smaller by bucketing, or detecting a duplicate/missing value by comparing counts against `1..n`. (Where values are bounded to `[1,n]`, [[Index Sign-Marking]] does the same job in O(1) space by encoding the count-bit into the array itself.)

**3. Hashmap-backed data structures** — a `value -> index` map layered over a dynamic array gives O(1) `insert` / `remove` / `getRandom` (swap-with-last on delete, then fix the moved element's index in the map).

**When it's the wrong tool:** if values are bounded to `[1,n]` and O(1) space is required, prefer [[Index Sign-Marking]]; if you only need the strict-majority element, [[Boyer-Moore Voting Algorithm]] avoids the map entirely.

## DSA problems
- [[Two Sum]] (LC 1) — complement lookup: store `value → index`, check for `target − x`.
- [[Majority Element]] (LC 169) — frequency count until a tally exceeds n/2 (hashmap alternative to Boyer-Moore).
- [[Insert Delete GetRandom O(1)]] (LC 380) — `value → index` map beside a vector for O(1) insert/remove/getRandom.
- [[Find All Numbers Disappeared in an Array]] (LC 448) — tally counts of `1..n`; missing values have count 0.
- [[Subarray Sum Equals K]] (LC 560) — prefix-sum frequency map; look up `runningSum − k`.
- [[Set Mismatch]] (LC 645) — counts of `1..n` reveal the value seen twice (dup) and never (missing).
- [[Jewels and Stones]] (LC 771) — hash-set of jewel chars, then O(1) membership per stone.
- [[Pairs of Songs With Total Durations Divisible by 60]] (LC 1010) — count remainders mod 60, pair each with its complement `(60 − r) % 60`.
- [[How Many Numbers Are Smaller Than the Current Number]] (LC 1365) — bucket-count values then prefix-accumulate to answer each query in O(1).
- [[The Two Sneaky Numbers of Digitville]] (LC 3289) — frequency count over `0..n-1`; the two values with count 2 are the sneaky pair.

## Related
[[Higher-Order Functions]] · [[Memoization]] · [[DSA for Web Development]] · [[Index Sign-Marking]] · [[Boyer-Moore Voting Algorithm]] · [[Prefix Sum]]

## Sources
- [[Bare Min DSA for WebDev]] — the O(n+m) vs O(n·m) parents/pets snippet and framing.
