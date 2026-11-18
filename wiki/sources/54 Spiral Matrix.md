---
type: source
area: sde
title: 54 Spiral Matrix
aliases: [54 Spiral Matrix, Spiral Matrix]
tags: [dsa, arrays, matrix]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/54 Spiral Matrix 106e9c4cbab880398c25e0525388f116.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Return all elements of a matrix in spiral (clockwise) order. Keep four shrinking walls — up, right, down, left — and a direction enum; traverse in the current direction until you hit a wall, then pull that wall inward and turn, until all m×n elements are collected.

## Approaches
- **Four walls + direction state machine** — maintain `UP_WALL`, `RIGHT_WALL`, `DOWN_WALL`, `LEFT_WALL` and a `direction`. A `switch` on the direction walks the current edge to its wall, steps back onto the last valid cell, moves the wall one step in, and rotates the direction. Loop until `count == row * col`. Time O(m·n), space O(1) (excluding output).

## Best solution
```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int row = matrix.size();
        int col = matrix[0].size();

        vector<int> res;
        enum Directions { UP, RIGHT, DOWN, LEFT };
        enum Directions direction = RIGHT;

        int UP_WALL = 0;
        int RIGHT_WALL = col;
        int DOWN_WALL = row;
        int LEFT_WALL = -1;

        int i = 0, j = 0;
        int count = 0;

        while (count < row * col) {
            switch (direction) {
                case RIGHT:
                    while (j < RIGHT_WALL) { res.push_back(matrix[i][j++]); count++; }
                    i++; j--; RIGHT_WALL--; direction = DOWN;
                    break;
                case DOWN:
                    while (i < DOWN_WALL) { res.push_back(matrix[i++][j]); count++; }
                    i--; j--; DOWN_WALL--; direction = LEFT;
                    break;
                case LEFT:
                    while (j > LEFT_WALL) { res.push_back(matrix[i][j--]); count++; }
                    i--; j++; LEFT_WALL++; direction = UP;
                    break;
                case UP:
                    while (i > UP_WALL) { res.push_back(matrix[i--][j]); count++; }
                    i++; j++; UP_WALL++; direction = RIGHT;
            }
        }

        return res;
    }
};
```
Optimal because each cell is visited exactly once — O(m·n) — with only four integer walls and a direction as state.

## Notes
- The note flags this as an Amazon question.
- Key subtlety: `UP_WALL` starts at 0 (not -1) because the first left-to-right pass over row 0 will push the up-wall to row 1 anyway, so it must begin already "used up" to 0.
- After each edge, the code steps `i`/`j` back onto the last valid cell before turning, then adjusts for the next direction's start — this back-and-forth is what keeps the pointer on the grid across turns.

## Techniques
[[Matrix Traversal]]

## Sources
- [[54 Spiral Matrix]] raw note — `raw/notes/DSA/DSA/54 Spiral Matrix 106e9c4cbab880398c25e0525388f116.md`
