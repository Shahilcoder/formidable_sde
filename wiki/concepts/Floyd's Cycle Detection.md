---
type: concept
area: sde
title: Floyd's Cycle Detection
aliases: [Floyd's Cycle Detection, Tortoise and Hare, Floyd's Algorithm]
tags: [dsa, arrays, linked-list, two-pointer]
status: draft
source_count: 1
created: 2026-07-12
updated: 2026-07-12
---

## Summary
Floyd's Cycle Detection (the "tortoise and hare") uses two pointers moving at different speeds to detect a cycle in a sequence of "next" pointers, and — with a second walk — to locate the cycle's **entrance**, all in O(n) time and O(1) space. It's the classic linked-list cycle tool, but it also cracks array problems that can be reframed as an implicit linked list.

## How it works
Two phases:

1. **Detect the meeting point.** Advance `slow` one step and `fast` two steps per iteration. If there's a cycle, the fast pointer laps the slow one and they meet inside the cycle.
2. **Find the entrance.** Reset a second pointer to the start and advance it and `slow` one step at a time; they meet exactly at the cycle's entrance. (This follows from the equal-distance identity between the head-to-entrance distance and the meeting-point-to-entrance distance.)

```cpp
int findDuplicate(vector<int>& nums) {
    int slow = 0, fast = 0;
    do {                            // phase 1: find meeting point
        slow = nums[slow];
        fast = nums[nums[fast]];
    } while (slow != fast);

    int slow2 = 0;                  // phase 2: find cycle entrance
    while (slow != slow2) {
        slow = nums[slow];
        slow2 = nums[slow2];
    }
    return slow;
}
```

**Why Floyd applies to LC 287 (Find the Duplicate Number).** The array holds `n + 1` values all in the range `[1, n]`, so the map `i -> nums[i]` acts as a "next pointer" over a **functional graph** (every node has exactly one outgoing edge). Because there are more values than distinct slots, some value repeats — and a repeated value means two different nodes point to the same successor. That shared successor creates a **cycle**, and the cycle's **entrance is precisely the duplicated value**. So: tortoise/hare (phase 1) finds a meeting point inside the cycle, and a second walk starting from index 0 (phase 2) converges with `slow` at the entrance, which is the duplicate. Index 0 is safe as the start because no value equals 0, so nothing points back into it — it can only be the tail leading into the cycle, never part of it.

## Problems
- [[Find the Duplicate Number]] (LC 287) — treat `i -> nums[i]` as a linked list over `[1, n]`; the duplicate is the cycle entrance found by tortoise/hare plus a second walk. O(1) space without mutating the array.

## Related
[[Two Pointer Technique]] · [[Index Sign-Marking]]

## Sources
- [[Find the Duplicate Number]] — the functional-graph framing and the two-phase tortoise/hare + entrance walk.
