---
type: source
area: sde
title: 1423 Maximum Points You Can Obtain from Cards
aliases: [1423 Maximum Points You Can Obtain from Cards, Maximum Points You Can Obtain from Cards]
tags: [dsa, arrays, sliding-window]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/1423 Maximum points obtain from card 140e9c4cbab880a8b161f07a658c5a90.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
You may take exactly `k` cards, each from either end of the row; maximize the total. Instead of choosing which ends to take, flip the problem: the cards you LEAVE form a contiguous window of size `n - k`. Minimize that window's sum — equivalently, slide a size-`(n-k)` window and maximize the sum of everything outside it.

## Approaches
- **Sliding window over the complement** — start the "kept" sum as the last `k` elements (window `[l=0, r=n-k)` left behind means we initially take the tail `k`). Then slide: each step subtract `cardPoints[r]` and add `cardPoints[l]`, advancing both, tracking the max taken sum. O(k) time after setup (O(n) total to build the first sum), O(1) space. The note states O(k) / O(1).

## Best solution
```cpp
class Solution {
public:
    int maxScore(vector<int>& cardPoints, int k) {
        int size = cardPoints.size();

        int l = 0;
        int r = size - k; // treat as [l, r)

        int max_sum = 0;
        for (int i = r; i < size; ++i) max_sum += cardPoints[i];

        int totalSum = max_sum;
        while (r < size) {
            totalSum = totalSum - cardPoints[r++] + cardPoints[l++];
            max_sum = max(totalSum, max_sum);
        }

        return max_sum;
    }
};
```
Optimal because it reframes the two-ended choice as a single fixed-size window that slides once, giving linear time and constant space instead of exploring exponential end-combinations.

## Notes
- The trick that makes it easy: taking `k` cards from the ends = leaving a contiguous middle block of `n - k`. Maximizing the taken sum = maximizing the complement of that block.
- The initial sum is the tail `k` elements; each slide trades one tail element for one head element, walking through every valid split.

## Techniques
[[Sliding Window]]

## Sources
- [[1423 Maximum Points You Can Obtain from Cards]] raw note — `raw/notes/DSA/DSA/1423 Maximum points obtain from card 140e9c4cbab880a8b161f07a658c5a90.md`
