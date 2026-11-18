---
type: concept
area: sde
title: Higher-Order Functions
aliases: [Higher-Order Functions, HOF, Higher Order Functions]
tags: [javascript, functional, arrays, web-dev]
status: draft
source_count: 1
created: 2026-07-12
updated: 2026-07-12
---

## Summary
**Higher-order functions** take a function as an argument and/or return a function. In day-to-day web work this mostly means the **array instance methods** — `map`, `filter`, `reduce`, `forEach`, `some`, `every`, `find`, `sort`, `flatMap` — which you should know cold.

## Details
- **`map`** — transform each element → new array of same length.
- **`filter`** — keep elements passing a predicate → shorter/equal array.
- **`reduce`** — fold the array into a single accumulated value (sum, group-by, build an object/map).
- **`find` / `some` / `every`** — search / existence / universal checks.
- **`sort`** — in-place ordering via a comparator (see the array `sort()` method).

`reduce` is the general primitive — `map` and `filter` can both be expressed as reductions. A common `reduce` idiom is building the index used by the [[Hashmap Lookup Pattern]].

**Beyond arrays**, HOFs also cover function-returning utilities like the closures behind [[Debouncing]], [[Throttling]], and [[Memoization]] — each returns a wrapped function. [[lodash]] packages many HOF utilities.

## Related
[[Hashmap Lookup Pattern]] · [[Memoization]] · [[lodash]] · [[DSA for Web Development]]

## Sources
- [[Bare Min DSA for WebDev]] — "map, filter, reduce and all other existing instance methods in arrays."
