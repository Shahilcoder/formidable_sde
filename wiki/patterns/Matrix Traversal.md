---
type: pattern
area: sde
title: Matrix Traversal
aliases: [Matrix Traversal]
tags: [dsa, arrays, matrix]
status: draft
source_count: 2
created: 2026-07-12
updated: 2026-07-12
---

## Summary
Techniques for walking or transforming a 2D grid with explicit index bookkeeping rather than recursion. Two recurring shapes: **spiral traversal** (visit the perimeter, shrink the boundary inward, repeat) and **rotate-in-place** (transpose across the diagonal, then reverse rows). Both hinge on maintaining boundary indices carefully and mutating the grid without an auxiliary matrix.

## How it works
**Spiral** — keep four walls (`UP`, `RIGHT`, `DOWN`, `LEFT`) and a direction. Walk in the current direction until you hit a wall, then pull that wall one step inward and turn clockwise; stop after collecting `m*n` cells:

```cpp
enum Directions { UP, RIGHT, DOWN, LEFT } direction = RIGHT;
int UP_WALL = 0, RIGHT_WALL = col, DOWN_WALL = row, LEFT_WALL = -1;
int i = 0, j = 0, count = 0;
while (count < row * col) {
    switch (direction) {
        case RIGHT: while (j < RIGHT_WALL) { res.push_back(matrix[i][j++]); count++; }
                    i++; j--; RIGHT_WALL--; direction = DOWN; break;
        // DOWN, LEFT, UP mirror this: consume the edge, step back, shrink the wall, turn
    }
}
```

**Rotate-in-place** — 90 degrees clockwise = transpose (swap `matrix[i][j]` with `matrix[j][i]` over one triangle) then reverse each row. This reuses the [[In-place Array Reversal]] row-reverse as its second step, so no extra O(n²) buffer is needed.

## Problems
- [[Rotate Image]] (LC 48) — transpose over the diagonal triangle, then reverse each row; O(1) space in-place rotation.
- [[Spiral Matrix]] (LC 54) — four shrinking walls + a direction enum collect the grid in spiral order, O(1) extra space.

## Related
[[In-place Array Reversal]]

## Sources
- [[Rotate Image]] — transpose + row-reverse rotation
- [[Spiral Matrix]] — four-wall directional spiral walk
