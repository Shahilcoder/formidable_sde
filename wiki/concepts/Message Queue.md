---
type: concept
area: sde
title: Message Queue
aliases: [Message Queue, Message Queues, Asynchronous Messaging]
tags: [system-design, message-queue, async, decoupling, reliability]
status: stub
source_count: 1
created: 2026-07-16
updated: 2026-07-16
---

## Summary
A **message queue** lets services communicate **asynchronously**: instead of Service A calling Service B and waiting for it to finish, A drops a message on a queue and moves on; B consumes it when ready. This decouples services and makes the system more reliable.

## Details
Example from [[Telusko Video Part 1]]: an Order Service needs to send an SMS. Rather than block on the (slow, possibly-down) SMS service, it publishes to a queue:
```
Order Service → Message Queue → SMS Service
```
The Order Service responds to the user immediately; the SMS is delivered whenever the SMS service picks up the message.

**Benefits:**
- **Decouples services** — producer and consumer don't need to be up at the same time or know about each other.
- **Handles retries** — a failed message can be redelivered.
- **Improves reliability** — work isn't lost if the consumer is temporarily down.
- **Supports asynchronous processing** — slow work happens off the critical request path.

**Common implementations:** RabbitMQ · Apache Kafka · Amazon SQS. *(Each to get its own entity page when a later source adds depth.)*

## Related
[[System Design Fundamentals]] · [[Monitoring & Observability]]

## Sources
- [[Telusko Video Part 1]] — Order → SMS async example; decoupling, retries, reliability; RabbitMQ / Kafka / SQS named.
