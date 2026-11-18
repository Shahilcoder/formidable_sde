---
type: source
area: sde
title: 1465 Maximum Area of a Piece of Cake
aliases: [1465 Maximum Area of a Piece of Cake, Maximum Area of a Piece of Cake]
tags: [dsa, arrays, greedy]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/1465 Maximum Area of Piece of Cake 16ce9c4cbab880a895a0ebec54539074.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Given horizontal and vertical cut positions on an `h × w` cake, find the largest resulting piece. The area of the biggest piece is (largest gap between consecutive horizontal cuts) × (largest gap between consecutive vertical cuts) — a greedy decomposition of the two dimensions, taken mod 1e9+7.

## Approaches
- **Sort + greedy max-gap** — sort both cut arrays, append the boundaries `h` and `w` (the cake's far edges are implicit cuts), then scan each array for the maximum difference between consecutive cuts. Multiply the two maxima and take modulo. O(H log H + V log V) time, O(1) extra space. (User's own first-shot accepted solution.)

## Best solution
```cpp
class Solution {
public:
    int maxArea(int h, int w, vector<int>& horizontalCuts, vector<int>& verticalCuts) {
        sort(horizontalCuts.begin(), horizontalCuts.end());
        sort(verticalCuts.begin(), verticalCuts.end());

        horizontalCuts.push_back(h);
        verticalCuts.push_back(w);

        long max_h = horizontalCuts[0];
        long max_w = verticalCuts[0];

        for (int i = 1, s = horizontalCuts.size(); i < s; ++i)
            max_h = max(max_h, (long)(horizontalCuts[i] - horizontalCuts[i - 1]));

        for (int i = 1, s = verticalCuts.size(); i < s; ++i)
            max_w = max(max_w, (long)(verticalCuts[i] - verticalCuts[i - 1]));

        return (max_h * max_w) % (1000000007);
    }
};
```
Optimal because the two dimensions are independent: the largest piece is bounded by the widest horizontal strip and the widest vertical strip, so maximizing each gap separately and multiplying is exact.

## Notes
- Initialize `max_h` / `max_w` to the FIRST cut position — that captures the gap from edge 0 to the first cut, which the consecutive-difference loop would otherwise miss.
- Append `h` and `w` so the final strip (last cut to the far edge) is counted.
- Use `long` for the gaps and the product before the modulo to avoid `int` overflow.

## Techniques
[[Greedy Algorithm]]

## Sources
- [[1465 Maximum Area of a Piece of Cake]] raw note — `raw/notes/DSA/DSA/1465 Maximum Area of Piece of Cake 16ce9c4cbab880a895a0ebec54539074.md`
