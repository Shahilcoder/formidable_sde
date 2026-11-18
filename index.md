---
type: index
area: sde
title: Index
updated: 2026-08-01
---

# Index

The content catalog for this wiki. Every wiki page is listed once under its category with a one-line summary. I read this first on every query and keep it current on every ingest. See [[CLAUDE]] for the rules and [[logs]] for the timeline.

---

## Maps
*Synthesis & overview pages (`wiki/maps/`).*
- [[DSA Patterns Overview]] — interview-prep hub: 39 solved LeetCode problems organized by transferable pattern.
- [[DSA for Web Development]] — core data structures & algos for web devs, each tied to a practical use case.
- [[System Design Fundamentals]] — hub for system design: the scaling ladder + the 7 core building blocks.

## Entities
*Named things — tech, libs, tools, people, orgs (`wiki/entities/`).*
- [[Trie]] — prefix tree; powers typeahead/autocomplete.
- [[Binary Tree]] — node + ≤2 children; terminology, types, linked vs `2i`/`2i+1` array layout, height conventions.
- [[Binary Search Tree]] — recursive left < node < right invariant; O(log N) search/insert/delete *if balanced*.
- [[Heap]] — priority queue backing; complete binary tree in an array, serves highest-priority items first.
- [[Queue]] — FIFO; backbone of async job/event processing, and the engine of BFS.
- [[Stack]] — LIFO; DFS made concrete, explicit or via the call stack.
- [[lodash]] — JS utility-belt library (collections, `debounce`/`throttle`, `keyBy`).

## Concepts
*Ideas, techniques, topics (`wiki/concepts/`).*
- [[Higher-Order Functions]] — `map`/`filter`/`reduce` & array methods; the daily web-dev primitives.
- [[Greedy Algorithm]] — local-optimal steps: intervals, jump games, stock trading, max-gap.
- [[Backtracking]] — decide → recurse → base → undo, for "generate ALL" problems.
- [[Tree Traversal]] — pre/in/post-order DFS (stack) and level-order BFS (queue); which order to pick when.
- [[Coordinate Compression]] — rank transform: map values to dense sorted ranks (1..k), ties shared; preprocessing for BIT/segment trees.
- [[Binary Exponentiation]] — halve the exponent for O(log n) power.
- [[Boyer-Moore Voting Algorithm]] — O(1)-space majority element via cancellation.
- [[Floyd's Cycle Detection]] — tortoise/hare; array-as-linked-list cycle entrance = duplicate.
- [[Bit Packing]] — pack two values into one int for O(1) extra space.
- [[Bounded Solution Space]] — constant answer universe → enumerate the whole catalog & filter → O(1).
- [[Scalability]] — the code → vertical → horizontal scaling ladder and its ceilings.
- [[Load Balancing]] — distribute requests across servers; health checks & failover.
- [[Caching]] — trade memory for latency on frequently accessed data.
- [[Data Consistency]] — single source of truth; why multiple servers need shared storage.
- [[Message Queue]] — async, decoupled service-to-service communication with retries.
- [[Monitoring & Observability]] — health, failure detection, debugging, performance across all components.

## Patterns
*Practical solutions, recipes, gotchas (`wiki/patterns/`).*
- [[Two Pointer Technique]] — converging-ends & slow/fast pointers; the dominant array pattern.
- [[k-Sum Pattern]] — sort + fix + two-pointer + dedup: Two Sum → 3Sum → 3Sum Closest → 4Sum.
- [[Sliding Window]] — fixed/variable window over a contiguous run.
- [[Prefix Sum]] — cumulative sums/products; prefix-sum + hashmap for subarray counting.
- [[Index Sign-Marking]] — encode "seen" in the array via sign; O(1) space.
- [[In-place Array Reversal]] — reverse-to-rotate/reorder.
- [[Matrix Traversal]] — spiral simulation & rotate-in-place.
- [[Hashmap Lookup Pattern]] — O(1) lookup by key; complement/frequency counting & hashmap-backed design (web-dev + DSA).
- [[Debouncing]] — fire once after a burst of events stops (search inputs, resize).
- [[Throttling]] — cap call rate to once per interval (scroll, mousemove).
- [[Memoization]] — cache pure-function results by args.
- [[LRU Cache]] — bounded cache with least-recently-used eviction; cache invalidation.

## Sources
*One summary per ingested raw source (`wiki/sources/`).*
- [[Bare Min DSA for WebDev]] — breadth checklist of minimum DSA for web devs, each structure tied to a use case.
- [[Telusko Video Part 1]] — intro to system design via the "Alien Bank" analogy; scaling ladder + 7 core building blocks.
- [[Binary Trees & Binary Search Trees]] — AlgoMap/Greg Hogg Lecture 8: tree structure, BST invariant, DFS/BFS traversals + complexities.

*DSA solved problems (Shahil's C++ LeetCode notes) — see [[DSA Patterns Overview]]:*
- [[1 Two Sum]] — complement hashmap for O(n) pair-sum; also sorted two-pointer.
- [[15 3Sum]] — sort + fix one + two-pointer, skip duplicates.
- [[16 3Sum Closest]] — two-pointer tracking min |target − sum|.
- [[18 4Sum]] — two fixed loops around two-pointer core, `long` overflow guard.
- [[26 Remove Duplicates from Sorted Array]] — slow/fast two-pointer in place.
- [[31 Next Permutation]] — find dip, swap next-greater, reverse suffix.
- [[45 Jump Game II]] — greedy minimum jumps.
- [[48 Rotate Image]] — transpose + reverse rows, in place.
- [[50 Pow(x, n)]] — binary exponentiation, O(log n).
- [[54 Spiral Matrix]] — four shrinking walls simulation.
- [[55 Jump Game]] — greedy reachability (goal-post).
- [[56 Merge Intervals]] — sort by start + linear merge sweep.
- [[78 Subsets]] — backtracking power-set construction.
- [[88 Merge Sorted Array]] — reverse three-pointer merge from the back.
- [[121 Best Time to Buy and Sell Stock]] — track running min price, max profit.
- [[122 Best Time to Buy and Sell Stock II]] — sum all positive consecutive diffs.
- [[125 Valid Palindrome]] — recursive two-pointer on filtered string.
- [[169 Majority Element]] — Boyer-Moore voting, O(1) space.
- [[189 Rotate Array]] — reverse-reverse-reverse in place.
- [[238 Product of Array Except Itself]] — prefix × suffix product, no division.
- [[283 Move Zeroes]] — slow/fast compaction of non-zeros.
- [[287 Find the Duplicate Number]] — Floyd's cycle detection on value→index graph.
- [[380 Insert Delete GetRandom O(1)]] — hashmap + vector, swap-with-last delete.
- [[415 Add Strings]] — schoolbook digit-by-digit addition with carry.
- [[448 Find All Numbers Disappeared in an Array]] — sign-marking (Claude-added canonical O(1)).
- [[560 Subarray Sum Equals K]] — prefix sum + hashmap of prefix counts, seed `{0:1}`.
- [[645 Set Mismatch]] — sign-marking / sum-and-sum-of-squares equations.
- [[724 Find Pivot Index]] — running total minus left (Claude-resolved O(1) trick).
- [[771 Jewels and Stones]] — hash-set membership count.
- [[977 Squares of a Sorted Array]] — two-pointer from both ends, fill from back.
- [[1010 Pairs of Songs With Total Durations Divisible by 60]] — remainder counting mod 60.
- [[1291 Sequential Digits]] — enumerate the 36 fixed sequential-digit numbers, filter to [low, high]; O(1).
- [[1331 Rank Transform of an Array]] — coordinate compression / rank transform; four value→rank mappings.
- [[1365 How Many Numbers Are Smaller Than the Current Number]] — counting tally + prefix sum.
- [[1423 Maximum Points You Can Obtain from Cards]] — slide the unpicked complement window.
- [[1465 Maximum Area of a Piece of Cake]] — max gaps between sorted cuts, greedy.
- [[1470 Shuffle the Array]] — bit-packing two values per int, O(1) space.
- [[1480 Running Sum of 1d Array]] — in-place prefix sum.
- [[1492 The kth Factor of n]] — √n divisor enumeration with perfect-square edge case.
- [[1752 Check if Array Is Sorted and Rotated]] — circular drop-count ≤ 1.
- [[3289 The Two Sneaky Numbers of Digitville]] — hash-set / sorted-adjacent duplicate detection.

