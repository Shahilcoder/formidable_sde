---
type: concept
area: sde
title: Caching
aliases: [Caching, Cache]
tags: [system-design, caching, performance, latency]
status: stub
source_count: 1
created: 2026-07-16
updated: 2026-07-16
---

## Summary
A **cache** stores frequently accessed data in a fast, close-at-hand layer so repeated reads don't have to hit the (slower) database every time. It trades a little memory for a lot of latency.

## Details
Sits between the backend and the database in the request path: `Client → Backend → Cache → Database`. The backend checks the cache first; on a hit it returns immediately, on a miss it falls through to the database (and typically populates the cache).

**Benefits:**
- Faster responses (data served from memory, not disk/DB).
- Fewer database queries → less load on the DB.
- Lower overall latency.

> Related client-side/app-level caching techniques already in this wiki: [[Memoization]] (cache pure-function results) and [[LRU Cache]] (bounded cache with least-recently-used eviction) — the same idea applied at code scale.

## Related
[[System Design Fundamentals]] · [[Memoization]] · [[LRU Cache]] · [[Data Consistency]]

## Sources
- [[Telusko Video Part 1]] — cache as a core building block; placement between backend and DB.
