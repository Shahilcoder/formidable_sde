---
type: source
area: sde
title: 48 Rotate Image
aliases: [48 Rotate Image, Rotate Image]
tags: [dsa, arrays, matrix]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/48 Rotate Image 10be9c4cbab88005a3f4df50fa9016c9.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Rotate an n×n matrix 90° clockwise in place. The trick is two in-place operations: transpose the matrix (swap across the main `\` diagonal), then reverse each row.

## Approaches
- **Transpose + reverse rows** — swap every element with its mirror across the main diagonal (iterate the upper or lower triangle only), then reverse each row left-to-right. Together this produces a clockwise rotation. Time O(n²), space O(1).

## Best solution
```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int rows = matrix.size();
        int cols = matrix[0].size();

        // transpose: swap across the main \ diagonal (upper triangle)
        for (int i = 0; i < rows; ++i) {
            for (int j = i + 1; j < cols; ++j)
                swap(matrix[i][j], matrix[j][i]);
        }

        // reverse each row
        for (auto &row : matrix) reverse(row.begin(), row.end());
    }
};
```
Optimal because both passes are in place with no auxiliary matrix — O(1) extra space, O(n²) work (unavoidable, every cell must move).

## Notes
- Iterating only the upper triangle (`j = i+1`) is essential; scanning the full matrix would swap each pair twice and undo the transpose. The lower-triangle variant (`j < i`) is equivalent.
- Transpose + reverse-rows = clockwise; for counter-clockwise you'd instead reverse rows first (or reverse each column).
- Attributed in the note to "Mafizuddin and My Approach".

## Techniques
[[Matrix Traversal]] · [[In-place Array Reversal]]

## Sources
- [[48 Rotate Image]] raw note — `raw/notes/DSA/DSA/48 Rotate Image 10be9c4cbab88005a3f4df50fa9016c9.md`
