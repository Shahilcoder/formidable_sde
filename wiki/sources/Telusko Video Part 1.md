---
type: source
area: sde
title: Telusko Video Part 1
aliases: [Telusko Video Part 1, Telusko System Design Part 1, Alien Bank Example]
tags: [system-design, scalability, load-balancing, caching, message-queue, fundamentals]
status: draft
source_type: talk
url: https://youtu.be/Vnm-ycSfJx4?si=3uHFLfIs_Rz8F-c4
author: Telusko
raw_path: raw/notes/System Design/Telusko Video Part 1.md
ingested: 2026-07-16
created: 2026-07-16
updated: 2026-07-16
---

## TL;DR
An intro-level system-design walkthrough that teaches the fundamentals through an **"Alien Bank"** analogy. A single cashier at a single counter is progressively scaled to handle growing traffic, and each fix maps to a real system-design concept: optimize the **code** first, then **scale vertically** (bigger server), then **scale horizontally** (more servers) — which in turn forces a **centralized database** (for consistency) and a **load balancer** (for even distribution). It closes by enumerating the **7 core building blocks** of a system and stitching them into one end-to-end request path.

## Key points
- **System = Components + Common Goal.** The bank (counter, cashier, customers) is the running metaphor for a software system.
- **The scaling ladder** — the video's spine, applied in order:
  1. **Code optimization** — train the cashier / write better algorithms (LLD, [[DSA Patterns Overview|DSA]], code quality). Cheapest first lever.
  2. **[[Scalability|Vertical scaling]]** — bigger counter, cash-counting machine, pre-filled forms / more RAM, faster CPU, better SSD. Hits a **hard ceiling**.
  3. **[[Scalability|Horizontal scaling]]** — add more counters / more servers. Effectively unlimited, but has prerequisites.
- **Horizontal scaling's two prerequisites:**
  - **[[Data Consistency|Shared/centralized database]]** — two counters with separate records let a customer withdraw twice; a single source of truth fixes it.
  - **[[Load Balancing|Load balancer]]** — customers naturally crowd Counter 1 while Counter 2 idles; a "middleman" distributes evenly, runs health checks, and routes around failed counters.
- **The bank → system mapping:** Customers = requests/traffic · Queue = incoming traffic · Cashier = application code · Cash Counter = server · Shared Records = centralized database · Middleman = load balancer.
- **7 core building blocks:** [[Data Consistency|Database]] (SQL / NoSQL) · Application/Backend layer (exposes APIs — GET/POST/PUT/DELETE, holds business logic, hides DB complexity) · Client (web/mobile/desktop/ATM) · [[Caching|Cache]] (frequently accessed data → lower latency, fewer DB queries) · [[Load Balancing|Load Balancer]] · [[Message Queue]] (async, decouples services, retries — RabbitMQ / Kafka / Amazon SQS) · [[Monitoring & Observability|Monitoring & Logging]].
- **End-to-end architecture:** Client → Load Balancer → Server1/Server2 → Cache → Database → Message Queue → External Services (SMS/Email), with Monitoring & Logging across everything.

## Notable quotes / data
> 10 min → 5 min/customer (code optimization) → 3 min/customer (vertical scaling) → parallel counters (horizontal scaling).

> Cashier: 10 min/customer = only 6 customers/hour. The 10th customer waits ~27 minutes even at 3 min/customer with one counter.

## Touches
[[System Design Fundamentals]] · [[Scalability]] · [[Load Balancing]] · [[Caching]] · [[Data Consistency]] · [[Message Queue]] · [[Monitoring & Observability]]
