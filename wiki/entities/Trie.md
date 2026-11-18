---
type: entity
area: sde
title: Trie
aliases: [Trie, Prefix Tree]
tags: [dsa, data-structures, strings, web-dev]
status: stub
source_count: 1
created: 2026-07-12
updated: 2026-07-12
---

## Summary
A **trie** (prefix tree) is a tree where each node represents a character and each path from the root spells a prefix. It gives fast prefix queries — lookup/insert is O(length of the key), independent of how many words are stored.

## Details
**Web use case:** typeahead / **autocomplete** and search suggestions — walk the trie to the typed prefix, then collect the words in its subtree. Also spell-check and IP routing tables.

Trade-off: fast prefix search at the cost of memory (many nodes/pointers). For simple cases a sorted list + binary search or a server-side search index may suffice.

## Related
[[DSA for Web Development]]

## Sources
- [[Bare Min DSA for WebDev]] — "Tries (prefix Tree) — for typeahead lookup; autocompletes; search suggestions."
