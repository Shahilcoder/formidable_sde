---
type: pattern
area: sde
title: Throttling
aliases: [Throttling, Throttle]
tags: [web-dev, performance, events, rate-limiting]
status: draft
source_count: 1
created: 2026-07-12
updated: 2026-07-12
---

## Summary
**Throttling** caps how often a function can run to at most once per interval, no matter how many times it's triggered. It guarantees a steady maximum rate during a continuous burst.

## Details
Classic web use cases: `scroll` and `mousemove` handlers, infinite-scroll trigger checks, firing analytics/telemetry at a bounded rate, rate-limiting API calls.

```js
function throttle(fn, interval) {
  let last = 0;
  return (...args) => {
    const now = Date.now();
    if (now - last >= interval) {
      last = now;
      fn(...args);
    }
  };
}
```

**Throttle vs [[Debouncing]]:** throttle fires *periodically during* the burst; debounce fires *once after* it ends. Use throttle when you want regular updates while something keeps happening (scroll position), debounce when you only care about the final state (search input).

## Related
[[Debouncing]] · [[DSA for Web Development]]

## Sources
- [[Bare Min DSA for WebDev]] — listed under "Other Algos" and Stacks & Queues as a core web algo.
