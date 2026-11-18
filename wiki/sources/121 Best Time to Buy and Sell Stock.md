---
type: source
area: sde
title: 121 Best Time to Buy and Sell Stock
aliases: [121 Best Time to Buy and Sell Stock, Best Time to Buy and Sell Stock]
tags: [dsa, arrays, greedy]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/121 Best Time to Buy and Sell Stock ab3cbaae5025480092c2493d6d20309d.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Given daily prices, find the max profit from a single buy-then-sell. The winning idea: one pass tracking the minimum price seen so far and the best profit achievable by selling today.

## Approaches
- **Single-pass min tracking (O(n) time, O(1) space):** as you scan, keep the running `min_price`; the best you could do selling on day `i` is `prices[i] - min_price`. Keep the max of those.

## Best solution
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int max_profit = 0;
        int min_price = INT_MAX;

        for (int i = 0; i < prices.size(); ++i) {
            min_price = min(min_price, prices[i]);
            max_profit = max(max_profit, prices[i] - min_price);
        }

        return max_profit;
    }
};
```
Optimal because it's a single linear pass with two scalar variables — no need to precompute anything or look ahead.

## Notes
The reframing that unlocked it: instead of "buy at the min, then find the best later sell", fix the **sell** day (the current index) and ask for the cheapest buy among all previous days. Since `min_price` is updated before computing profit, buying and selling on the same day yields 0, which safely handles a monotonically decreasing price array.

## Techniques
[[Greedy Algorithm]]

## Sources
- [[121 Best Time to Buy and Sell Stock]] raw note — `raw/notes/DSA/DSA/121 Best Time to Buy and Sell Stock ab3cbaae5025480092c2493d6d20309d.md`
