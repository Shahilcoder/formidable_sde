---
type: pattern
area: sde
title: Debouncing
aliases: [Debouncing, Debounce]
tags: [web-dev, performance, events, rate-limiting]
status: draft
source_count: 1
created: 2026-07-12
updated: 2026-07-12
---

## Summary
**Debouncing** collapses a rapid burst of events into a single call that fires only after the activity *stops* for a set quiet period. Each new event resets the timer.

## Details
Classic web use cases: a **search-as-you-type** input (wait until the user pauses before hitting the API), window `resize`, form auto-save, validating a field after the user stops typing.

```js
function debounce(fn, delay) {
  let timer;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => fn(...args), delay);
  };
}
```

**Debounce vs [[Throttling]]:** debounce fires *once, after the burst ends*; throttle fires *at a steady max rate during* the burst. Rule of thumb — debounce for "wait until they're done" (search box); throttle for "do it periodically while it happens" (scroll handler).

## Related
[[Throttling]] · [[Memoization]] · [[DSA for Web Development]]

## Sources
- [[Bare Min DSA for WebDev]] — listed under "Other Algos" and Stacks & Queues as a core web algo.
