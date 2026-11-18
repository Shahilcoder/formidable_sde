---
type: map
area: sde
title: System Design Fundamentals
aliases: [System Design Fundamentals, System Design Overview, System Design]
tags: [system-design, scalability, fundamentals]
status: draft
created: 2026-07-16
updated: 2026-07-16
---

## Thesis
Designing a system is the art of taking a component that works for a handful of users and evolving it to serve millions **without rewriting it from scratch** at each step. The discipline is a **ladder of levers applied in order of cost**: optimize the code, then grow the machine, then multiply the machines — and each rung above the first forces new supporting infrastructure (shared storage, request distribution, caching, async messaging, observability). This map is the hub for that landscape; it grows as more sources arrive.

> A **system** is *components working together toward a common goal*. Everything below is a component; the goal is serving requests correctly, fast, and reliably at scale.

## The scaling ladder
Apply cheapest-first. Each rung is where the previous one runs out.

1. **Code optimization** — better algorithms, cleaner low-level design, efficient implementation ([[DSA Patterns Overview|DSA]] & LLD). No new hardware; always try this first.
2. **Vertical scaling** — make the one server bigger (RAM, CPU, SSD). Simple, but hits a **hard physical/cost ceiling**. See [[Scalability]].
3. **Horizontal scaling** — add more servers. Effectively unbounded throughput and better availability, but **requires** the supporting pieces below. See [[Scalability]].

Horizontal scaling's prerequisites:
- **[[Data Consistency|Shared database]]** — otherwise servers hold divergent state (double-withdrawal problem).
- **[[Load Balancing|Load balancer]]** — otherwise traffic pools unevenly and failed servers keep getting requests.

## The 7 core building blocks
- **Database** — store/retrieve/update/delete data; **SQL** vs **NoSQL** (each to get its own page when a source deepens it). Consistency angle: [[Data Consistency]].
- **Application / Backend layer** — exposes **APIs** (GET/POST/PUT/DELETE), holds business logic, hides DB complexity from clients.
- **Client** — web / mobile / desktop / ATM apps that call the backend APIs.
- **[[Caching|Cache]]** — keep frequently accessed data close → lower latency, fewer DB hits.
- **[[Load Balancing|Load Balancer]]** — even request distribution, health checks, failover.
- **[[Message Queue]]** — asynchronous, decoupled service-to-service communication with retries (RabbitMQ / Kafka / Amazon SQS).
- **[[Monitoring & Observability|Monitoring & Logging]]** — health, failure detection, debugging, performance, release verification — across every component.

## End-to-end request path
```
Client → Load Balancer → Server1 / Server2 → Cache → Database → Message Queue → External Services (SMS, Email)
                                   (Monitoring & Logging across all)
```

## Landscape
- [[Scalability]] — the code → vertical → horizontal ladder and its ceilings.
- [[Load Balancing]] — distributing requests across servers; health checks & failover.
- [[Caching]] — trading memory for latency on hot data.
- [[Data Consistency]] — single source of truth; why multiple servers need shared storage.
- [[Message Queue]] — async decoupling and reliable delivery between services.
- [[Monitoring & Observability]] — knowing what the running system is doing.

## Sources
- [[Telusko Video Part 1]] — intro via the Alien Bank analogy; seeded this map and all six landscape concepts.
