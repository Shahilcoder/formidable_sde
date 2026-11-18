---
type: map
area: sde
title: DSA Patterns Overview
aliases: [DSA Patterns Overview]
tags: [dsa, patterns, interview-prep]
status: draft
created: 2026-07-12
updated: 2026-08-01
---

## Thesis
Interview DSA is best studied by **transferable pattern**, not by problem. This map organizes the
solved LeetCode set (41 problems, all C++, from [[Bare Min DSA for WebDev|Shahil's notes]]) around the
handful of techniques that actually recur — so a new problem is recognized as "a k-Sum" or "a prefix
sum + hashmap" rather than solved from scratch. Each technique page carries the mechanics and every
problem that drills it; each problem's source page carries the worked solution and the optimal C++.

Distinct from [[DSA for Web Development]], which frames data structures by their day-job web use case.
This map is the interview-prep lens.

## How to use this
- Recognize the **pattern** first (below), then open the technique page for the recipe.
- Each problem links to its source page (worked solution + optimal C++ + your commentary).
- Difficulty and category tags drive Bases views (e.g. all `medium` array problems).

## Techniques (the recipes)

### Two-pointer family
- [[Two Pointer Technique]] — converging-ends & slow/fast; the single most-used pattern here (10 problems).
- [[k-Sum Pattern]] — sort + fix + two-pointer + dedup: the [[Two Sum]] → [[3Sum]] → [[3Sum Closest]] → [[4Sum]] ladder.
- [[Sliding Window]] — fixed/variable window over a contiguous run ([[Maximum Points You Can Obtain from Cards]]).

### Hashing
- [[Hashmap Lookup Pattern]] — complement counting, frequency counting, and hashmap-backed design (10 problems).
- [[Index Sign-Marking]] — encode "seen" in the array itself via sign; O(1) space ([[Set Mismatch]], [[Find All Numbers Disappeared in an Array]]).

### Prefix & running aggregates
- [[Prefix Sum]] — cumulative sums / products, and prefix-sum + hashmap for subarray counting (5 problems).
- [[Coordinate Compression]] — rank transform: replace values by their sorted rank, ties shared ([[Rank Transform of an Array]], cousin of [[How Many Numbers Are Smaller Than the Current Number]]).

### Greedy
- [[Greedy Algorithm]] — local-optimal steps: interval merge, jump games, stock trading, max-gap (7 problems).

### Matrix & in-place reordering
- [[Matrix Traversal]] — spiral simulation & rotate-in-place.
- [[In-place Array Reversal]] — reverse-to-rotate/reorder ([[Rotate Array]], [[Rotate Image]], [[Next Permutation]]).

### Recursion / divide & conquer
- [[Backtracking]] — decide → recurse → base → undo, for "generate ALL" ([[Subsets]]).
- [[Binary Exponentiation]] — halve the exponent for O(log n) power ([[Pow(x, n)]]).

### Trees
- [[Tree Traversal]] — the core recipe: pick the order (pre/in/post-order DFS, or level-order BFS) and do one line of work per node. Stack goes deep, [[Queue|queue]] goes wide.
- [[Binary Tree]] — node + ≤2 children; terminology, complete/perfect/full types, linked vs `2i`/`2i+1` array layout, and the height-convention trap.
- [[Binary Search Tree]] — the recursive left < node < right invariant; search/insert/delete, in-order-yields-sorted, and why "O(log N)" is a balance claim, not a BST claim.
- [[Stack]] — the structure DFS is made of, whether explicit or the recursive call stack.

*Theory only so far — no tree problems solved yet. See Gaps.*

### Enumeration
- [[Bounded Solution Space]] — when the answer universe is a provable constant, enumerate the whole catalog and filter → O(1) ([[1291 Sequential Digits]]).

### Named algorithms (single-problem, high-yield)
- [[Boyer-Moore Voting Algorithm]] — O(1)-space majority ([[Majority Element]]).
- [[Floyd's Cycle Detection]] — array-as-linked-list cycle entrance = duplicate ([[Find the Duplicate Number]]).
- [[Bit Packing]] — pack two values in one int for O(1) space ([[Shuffle the Array]]).

## Problems by category

### Arrays — Easy
[[Two Sum]] · [[Best Time to Buy and Sell Stock]] · [[Merge Sorted Array]] · [[Move Zeroes]] ·
[[Running Sum of 1d Array]] · [[Find Pivot Index]] · [[Majority Element]] · [[Squares of a Sorted Array]] ·
[[Remove Duplicates from Sorted Array]] · [[Check if Array Is Sorted and Rotated]] ·
[[The Two Sneaky Numbers of Digitville]] · [[Shuffle the Array]] · [[Set Mismatch]] ·
[[How Many Numbers Are Smaller Than the Current Number]] · [[Find All Numbers Disappeared in an Array]] ·
[[Rank Transform of an Array]]

### Arrays — Medium
[[Rotate Array]] · [[Merge Intervals]] · [[3Sum]] · [[Product of Array Except Itself]] ·
[[Insert Delete GetRandom O(1)]] · [[Subarray Sum Equals K]] · [[Next Permutation]] · [[Spiral Matrix]] ·
[[Rotate Image]] · [[3Sum Closest]] · [[Pairs of Songs With Total Durations Divisible by 60]] · [[4Sum]] ·
[[Find the Duplicate Number]] · [[Jump Game]] · [[Jump Game II]] ·
[[Maximum Points You Can Obtain from Cards]] · [[Maximum Area of a Piece of Cake]] · [[The kth Factor of n]] ·
[[Best Time to Buy and Sell Stock II]] · [[Sequential Digits]]

### Recursion
[[Valid Palindrome]] (Easy) · [[Pow(x, n)]] (Medium) · [[Subsets]] (Medium)

### String
[[Add Strings]] (Easy) · [[Jewels and Stones]] (Easy)

## Gaps & follow-ups
- Study cadence lives in the [[Bare Min DSA for WebDev|raw DSA index note]] (Easy 5-10 min, Medium 20 min, Hard 30-45 min; note in 5, else X+5+5).
- Categories present: Arrays (dominant), Recursion, String, and **Trees (theory only)**. Not yet covered:
  linked lists, graphs, DP, heaps/[[Heap]], [[Trie]] — candidates for the next ingest.
- **Trees need problems.** [[Binary Trees & Binary Search Trees]] gave the theory; the drill set is missing.
  High-yield next: Maximum Depth, Invert Binary Tree, Same Tree, Validate BST, Kth Smallest in a BST,
  Level Order Traversal, Lowest Common Ancestor, Diameter of a Binary Tree.
- **Binary search has no page yet.** The AlgoMap clipping carried Lecture 7's C++ binary-search code, but it
  was out of scope for a trees ingest — needs its own source, covering both the classic target search and the
  condition-based "first index where the predicate holds" (lower-bound) form.
- **Self-balancing trees** (AVL, red-black — what `std::map` actually is) are the unfilled hole behind every
  O(log N) claim on [[Binary Search Tree]].
- [[Find All Numbers Disappeared in an Array]] and [[Find Pivot Index]] carry Claude's additions
  (canonical O(1) approaches the raw notes were missing / unsure about).
