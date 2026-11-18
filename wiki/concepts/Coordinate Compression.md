---
type: concept
area: sde
title: Coordinate Compression
aliases: [Coordinate Compression, Rank Transform, Coordinate Compression (Rank Transform)]
tags: [dsa, sorting, hashmap, binary-search, competitive-programming]
status: draft
source_count: 1
created: 2026-07-12
updated: 2026-07-12
---

## Summary
**Coordinate compression** (a.k.a. **rank transform**) replaces each value in a collection with its **rank** in sorted order — the smallest distinct value maps to 1, the next distinct value to 2, and so on, with **equal values sharing a rank**. It squeezes an arbitrary set of `k` distinct values (which may be huge, negative, or sparse — e.g. up to 10⁹) into the dense range `1..k` while preserving relative order. That "same order, small numbers" property is what makes it useful.

## Details

### Why it matters
Many structures index by *value* — a Binary Indexed Tree (Fenwick), a segment tree, or a plain counting/bucket array — and need those values to be small, dense, non-negative indices. Coordinate compression is the standard preprocessing step that makes such structures applicable to values that are otherwise too large or too spread out to index directly. It's a staple of competitive programming (counting inversions, range queries over sparse coordinates, sweep-line events).

### The recipe (sort + dedup + map back)
1. **Sort** a copy of the values.
2. **Deduplicate** so you have the distinct values in increasing order. In C++: `sorted.erase(unique(sorted.begin(), sorted.end()), sorted.end())`.
3. **Map each original value to its rank** = its position in the distinct-sorted array. Either
   - **binary search**: `lower_bound(sorted.begin(), sorted.end(), x) - sorted.begin()` gives the 0-based rank (`+1` for 1-based), or
   - **hashmap**: precompute `value → rank` in one pass over the distinct array for O(1)-average lookups, or
   - **ordered map** (`std::map`): insert all values, then one in-order pass assigns ranks implicitly.

All variants are **O(n log n)** (dominated by the sort) and **O(n)** space.

### Ties: shared rank vs. distinct rank
The defining question is what happens to equal values. In the standard rank transform ([[1331 Rank Transform of an Array]]) **equal values share a rank** — dedup before ranking. If instead every element needs a *unique* rank (a stable total order), don't dedup: sort `(value, originalIndex)` pairs and assign ranks by sorted position, breaking ties by index.

### Relation to "count smaller"
Rank is closely tied to *counting how many values are smaller*. In [[1365 How Many Numbers Are Smaller Than the Current Number]], the answer for a value is the number of elements strictly less than it — essentially a rank measured in *elements* rather than *distinct values*. When the value range is small and bounded, a counting-array + [[Prefix Sum]] beats sorting and gives O(n).

## Related
[[Hashmap Lookup Pattern]] · [[Prefix Sum]] · [[1365 How Many Numbers Are Smaller Than the Current Number]] · [[DSA Patterns Overview]]

## Sources
- [[1331 Rank Transform of an Array]] — four ways to compute the rank map (hashmap, sorted pairs, `lower_bound`, `std::map`); the `lower_bound` position-as-rank idiom is the canonical form.
