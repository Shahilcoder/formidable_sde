---
type: entity
area: sde
title: Queue
aliases: [Queue, FIFO Queue]
tags: [dsa, data-structures, async, web-dev, trees]
status: draft
source_count: 2
created: 2026-07-12
updated: 2026-08-01
---

## Summary
A **queue** is a FIFO (first-in, first-out) structure: items are enqueued at one end and dequeued from the other. Enqueue/dequeue are O(1).

## Details
**Web use case:** **async job/event processing.** Producers push events/jobs onto the queue; a worker process dequeues them one at a time, processes each, and flags it as done. This decouples request handling from slow work (email sending, image processing, webhooks) and smooths load spikes — the backbone of message queues and background job systems.

Related structures: a [[Heap]] backs a *priority* queue (dequeue by importance, not arrival order); a [[Stack]] is the LIFO counterpart.

**DSA use case:** a queue *is* breadth-first search. BFS / level-order [[Tree Traversal|traversal]] enqueues a node's children as it dequeues the node, so nodes come out in level-by-level order — the same loop as iterative DFS with a [[Stack]] swapped in. FIFO goes wide, LIFO goes deep. On an unweighted graph this is also what makes BFS find shortest paths.

## Related
[[Heap]] · [[Stack]] · [[Tree Traversal]] · [[Binary Tree]] · [[Message Queue]] · [[DSA for Web Development]]

## Sources
- [[Bare Min DSA for WebDev]] — "Async processes/jobs uses queue... the worker process dequeues and processes them, and flags it as done."
- [[Binary Trees & Binary Search Trees]] — BFS is queue-driven; level-order traversal code and its O(N) space bound (widest level).
