---
type: source
area: sde
title: 1331 Rank Transform of an Array
aliases: [1331 Rank Transform of an Array, Rank Transform of an Array]
tags: [dsa, arrays, sorting, hashmap, binary-search, coordinate-compression]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/1331 Rank Transform of an Array.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Replace every element with its **rank** in sorted order: the smallest distinct value becomes 1, the next distinct value 2, and so on, with **equal values sharing the same rank**. This is textbook [[Coordinate Compression]] (rank transform). Every approach is O(n log n) — the sort dominates — and they differ only in *how* they map each value to its rank. The four solutions here are a nice tour of that one design decision.

## Approaches
All four are **O(n log n) time, O(n) space**.

- **1 — Sort copy + `unordered_map` + rank counter.** Sort a copy, walk it once assigning each *new* value the next rank via a separate counter, then rewrite the original by hashmap lookup. Fastest in practice (O(1) average lookups).
- **2 — Sort `(value, index)` pairs, no hashmap.** Carry each element's original index through the sort. After sorting, walk left→right; bump the rank whenever the value changes, and write the rank straight back to `res[pairs[i].second]`. Avoids the hashmap entirely by remembering where each value came from.
- **3 — Sort + `unique`/`erase` + `lower_bound`.** Build a sorted array of the **distinct** values, then each element's rank is just *its position in that distinct-sorted array + 1*, found by binary search. The canonical coordinate-compression idiom (see the walkthrough below).
- **4 — `std::map` (red-black tree).** Insert every value as a key (auto-sorted, auto-deduped), do one in-order pass assigning ranks, then rewrite by lookup. Most concise — sorting and dedup happen implicitly — but the tree's constant factors lag `unordered_map`.

## Best solution
Approach 1 is the best **in practice** (simple, cache-friendly copy sort, O(1)-average lookups):

```cpp
class Solution {
public:
    vector<int> arrayRankTransform(vector<int>& arr) {
        unordered_map<int, int> mp;
        vector<int> res = arr;
        int size = res.size();

        sort(res.begin(), res.end());

        int rank = 1;                       // separate rank counter
        for (int i = 0; i < size; ++i)
            if (mp.find(res[i]) == mp.end())
                mp[res[i]] = rank++;        // first time we see a value → next rank

        for (int i = 0; i < size; ++i) res[i] = mp[arr[i]];
        return res;
    }
};
```

The one worth *learning* is Approach 3 — it generalizes to compressing coordinates before a BIT / segment tree (see [[Coordinate Compression]]).

## Approach 3 — the `lower_bound` line, explained
Your note says *"complicated, I don't understand this"* on this line:

```cpp
int rank = lower_bound(sorted.begin(), sorted.end(), arr[i]) - sorted.begin() + 1;
```

Read it in three moves, given `sorted` now holds only the **distinct** values in increasing order:

1. `lower_bound(sorted.begin(), sorted.end(), arr[i])` returns an **iterator** to the first element **≥ `arr[i]`**. Because `arr[i]` is guaranteed to be *in* `sorted`, this points exactly at `arr[i]`.
2. `... - sorted.begin()` converts that iterator to a **0-based index** — the position of `arr[i]` among the distinct sorted values (pointer arithmetic; the distance from the start).
3. `... + 1` shifts to a **1-based rank**, because the problem wants ranks starting at 1.

So "position of the value in the distinct-sorted array" **is** the rank — that's the whole trick. Example: `sorted = [10, 20, 30, 40]`. For `arr[i] = 30`, `lower_bound` lands at index 2, `+1` → rank **3**. ✓

The `unique` + `erase` step above it is the standard C++ dedup idiom, and your note already nails it:

```cpp
sorted.erase(unique(sorted.begin(), sorted.end()), sorted.end());
```

`unique` doesn't shrink the vector — it moves the distinct values to the front and returns an iterator to the new logical end (everything past it is leftover garbage). `erase(that_iterator, end())` then physically drops the tail. `unique` only removes **adjacent** duplicates, which is why the array must be **sorted first**.

### `upper_bound` variant (equivalent)
`upper_bound` returns the first element **strictly greater than** `arr[i]` — one step past `lower_bound`. On the deduplicated array that lands exactly on the "+1", so you drop the `+ 1` and get the same rank:

```cpp
for (int i = 0; i < arr.size(); i++) {
    int rank = upper_bound(sorted.begin(), sorted.end(), arr[i]) - sorted.begin();
    res[i] = rank;
}
```

| | points at | `... - begin()` |
|---|---|---|
| `lower_bound(x)` | `x` itself | index of `x`; needs `+ 1` |
| `upper_bound(x)` | element after `x` | index of `x` `+ 1` = rank directly |

**This equivalence holds only because `sorted` is deduplicated** — every value appears once, so `upper_bound - lower_bound == 1`. Skip the `unique`/`erase` and they diverge: on an array *with* duplicates, `lower_bound(x)` is the first occurrence and `upper_bound(x)` is just past the last, so `upper - lower` = the **count of `x`** (the standard "frequency in a sorted array" idiom). For rank transform you always dedup first, so either function works.

## Notes
- **Ties share a rank** — that's the defining rule. Approach 1 handles it by only assigning a rank the *first* time a value is seen; approach 2 by only bumping `rank` when the value changes; approaches 3 & 4 by deduping before ranking.
- Approach 2's trick — sorting `(value, index)` pairs to remember where each element came from — is a reusable move whenever you sort but must write results back in original positions.
- Cousin problem: [[1365 How Many Numbers Are Smaller Than the Current Number]] is the same "rank via sorting" family. 1331's rank ≈ *1 + (number of distinct values smaller)*; 1365 counts *all* smaller elements.

## Comparison
| # | Value→rank mechanism | In practice |
|---|----------------------|-------------|
| 1 | sort copy + `unordered_map` | Fastest; O(1) avg lookups, no ordering during insert |
| 2 | sort `(value,index)` pairs | No hashmap; carries the original index through the sort |
| 3 | sort + `unique` + `lower_bound` | Keeps a reusable distinct-sorted array; canonical compression |
| 4 | `std::map` in-order pass | Most concise; red-black tree constants lag `unordered_map` |

## Techniques
[[Coordinate Compression]] · [[Hashmap Lookup Pattern]]

## Sources
- [[1331 Rank Transform of an Array]] raw note — `raw/notes/DSA/DSA/1331 Rank Transform of an Array.md`
