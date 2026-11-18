---
type: concept
area: sde
title: Data Consistency
aliases: [Data Consistency, Single Source of Truth, Centralized Database]
tags: [system-design, data-consistency, databases, scalability]
status: stub
source_count: 1
created: 2026-07-16
updated: 2026-07-16
---

## Summary
**Data consistency** means every part of a system sees the same, correct data. The moment you [[Scalability|scale horizontally]] to multiple servers, keeping their view of the data consistent becomes a first-class problem — and the baseline fix is a **centralized (shared) database** acting as a single source of truth.

## Details
In the [[Telusko Video Part 1|bank analogy]], two counters each keeping **separate** records is a disaster: Counter 2 doesn't know a customer already withdrew at Counter 1, so the customer can **withdraw twice**. The data has diverged.

**Fix — centralized database:** both counters read and write the *same* store.
```
Counter 1 ┐
          ├─ Database (single source of truth)
Counter 2 ┘
```

**Benefits:**
- Shared customer data across all servers.
- Consistent balances / state.
- One authoritative source of truth.

This is the reason horizontal scaling can't just be "add servers" — the servers must be **stateless** and share their state through common storage.

## Related
[[System Design Fundamentals]] · [[Scalability]] · [[Caching]]

## Sources
- [[Telusko Video Part 1]] — the double-withdrawal problem and the centralized-database fix.
