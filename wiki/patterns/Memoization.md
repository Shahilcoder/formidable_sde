---
type: pattern
area: sde
title: Memoization
aliases: [Memoization, Memoize]
tags: [web-dev, performance, caching, dynamic-programming]
status: draft
source_count: 1
created: 2026-07-12
updated: 2026-07-12
---

## Summary
**Memoization** caches the result of a pure function keyed by its arguments, so repeated calls with the same inputs return instantly instead of recomputing.

## Details
```js
function memoize(fn) {
  const cache = new Map();
  return (...args) => {
    const key = JSON.stringify(args);
    if (cache.has(key)) return cache.get(key);
    const result = fn(...args);
    cache.set(key, result);
    return result;
  };
}
```

Web use cases: memoizing expensive pure computations, React's `useMemo`/`memo`/`useCallback` to avoid re-renders and recomputation, caching derived selectors. It's also the engine behind top-down **dynamic programming** (cache subproblem results).

**Caveats:** only sound for pure functions (same input → same output, no side effects). An unbounded cache is a memory leak — for bounded caching with eviction, use an [[LRU Cache]]. Key generation matters: `JSON.stringify` is fine for simple args but breaks on object identity/order and non-serializable values.

## Related
[[LRU Cache]] · [[Hashmap Lookup Pattern]] · [[Caching]] — the same idea at system scale · [[DSA for Web Development]]

## Sources
- [[Bare Min DSA for WebDev]] — listed under "Other Algos".
