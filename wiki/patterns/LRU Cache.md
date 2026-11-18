---
type: pattern
area: sde
title: LRU Cache
aliases: [LRU Cache, Least Recently Used, LRU]
tags: [web-dev, caching, cache-invalidation, data-structures, interview]
status: draft
source_count: 1
created: 2026-07-12
updated: 2026-07-12
---

## Summary
An **LRU (Least Recently Used) cache** is a fixed-capacity cache that evicts the entry that hasn't been accessed for the longest time when it's full. It's the standard answer to **cache invalidation** under a memory bound.

## Details
Web use cases: bounding a [[Memoization]] cache, in-memory API response caches, image/asset caches, session or route caches — anywhere you want caching's speed without unbounded memory growth.

**Interview-standard implementation:** a **hash map + doubly linked list**, giving O(1) `get` and `put`.
- The hash map maps key → node for O(1) lookup.
- The doubly linked list orders nodes by recency; most-recently-used at the head, LRU at the tail.
- On `get`/`put`, move the touched node to the head; on overflow, evict the tail.

In JS, a `Map` preserves insertion order, so a compact LRU can be built by deleting-and-reinserting keys on access and evicting `map.keys().next().value` (the oldest) when over capacity.

**Cache invalidation** more broadly is "one of the two hard things in CS" — LRU is the eviction *policy*; other policies (LFU, TTL/expiry, write-through) trade off differently.

## Related
[[Memoization]] · [[Hashmap Lookup Pattern]] · [[Caching]] — the eviction policy behind a system-level cache · [[DSA for Web Development]]

## Sources
- [[Bare Min DSA for WebDev]] — "Cache invalidation; LRU (Least recently used)" under Other Algos.
