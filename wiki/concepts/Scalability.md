---
type: concept
area: sde
title: Scalability
aliases: [Scalability, Vertical Scaling, Horizontal Scaling, Scaling Up, Scaling Out]
tags: [system-design, scalability, fundamentals]
status: draft
source_count: 1
created: 2026-07-16
updated: 2026-07-16
---

## Summary
**Scalability** is a system's ability to handle growing load without falling over. The core mental model is a **ladder of levers applied cheapest-first**: optimize the code, then grow the single machine (**vertical**), then multiply machines (**horizontal**). Each rung is where the previous one runs out.

## Details

### 1. Optimize the code first
Before spending on hardware, make the software do less work: better algorithms, cleaner low-level design, efficient implementation ([[DSA Patterns Overview|DSA]] / LLD). In the [[Telusko Video Part 1|bank analogy]]: train the cashier so a transaction drops from 10 min → 5 min. Always the first lever — it costs nothing but engineering.

### 2. Vertical scaling (scale up)
Make the **one** server more powerful: more RAM, faster CPU, better SSD. Bank analogy: a bigger counter, a cash-counting machine, pre-filled forms (5 min → 3 min).
- **Pros:** simple — no code changes, no distribution problems.
- **Con — the hard ceiling:** you eventually hit the biggest machine money can buy. A single machine is also a single point of failure.

### 3. Horizontal scaling (scale out)
Add **more** servers and run them in parallel. Bank analogy: open Counter 2, Counter 3, … . Effectively unbounded throughput, and redundancy means better availability.
- **Prerequisite 1 — [[Data Consistency|shared/centralized database]]:** independent servers with separate state diverge (a customer withdraws twice from two counters). All servers must read/write one source of truth.
- **Prerequisite 2 — [[Load Balancing|load balancer]]:** something must distribute requests evenly across servers and route around failed ones; otherwise traffic pools on one server.

### Vertical vs horizontal — the trade-off
| | Vertical (scale up) | Horizontal (scale out) |
|---|---|---|
| How | Bigger single machine | More machines |
| Complexity | Low | Higher (needs shared DB + LB) |
| Ceiling | Hard limit | Effectively unbounded |
| Availability | Single point of failure | Redundant |

## Related
[[System Design Fundamentals]] · [[Load Balancing]] · [[Data Consistency]] · [[Caching]]

## Sources
- [[Telusko Video Part 1]] — the code → vertical → horizontal ladder via the Alien Bank analogy; horizontal scaling's two prerequisites.
