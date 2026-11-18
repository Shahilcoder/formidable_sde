---
type: concept
area: sde
title: Load Balancing
aliases: [Load Balancing, Load Balancer]
tags: [system-design, load-balancing, scalability, availability]
status: stub
source_count: 1
created: 2026-07-16
updated: 2026-07-16
---

## Summary
A **load balancer** sits in front of a pool of servers and spreads incoming requests across them. It's the "middleman" that makes [[Scalability|horizontal scaling]] actually work: without it, traffic pools unevenly on whichever server clients happen to hit, and requests keep flowing to servers that have already failed.

## Details
In the [[Telusko Video Part 1|bank analogy]], customers naturally crowd Counter 1 while Counter 2 sits idle. A middleman who watches the queues and directs each customer to the least-busy counter — and stops sending anyone to a broken counter — is a load balancer.

**Core responsibilities:**
- **Even distribution** — route each request to an appropriate server (e.g. least-busy).
- **Health checks** — continuously probe servers to know which are alive.
- **Failover** — detect a failed server and route traffic away from it.

Positioned first in the request path: `Client → Load Balancer → Server1 / Server2 → …`.

## Related
[[System Design Fundamentals]] · [[Scalability]] · [[Monitoring & Observability]]

## Sources
- [[Telusko Video Part 1]] — introduced as the "middleman"; distribution, health checks, failover.
