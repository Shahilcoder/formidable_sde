---
type: source
area: sde
title: 122 Best Time to Buy and Sell Stock II
aliases: [122 Best Time to Buy and Sell Stock II, Best Time to Buy and Sell Stock II]
tags: [dsa, arrays, greedy]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/122 Best Time to Buy and Sell Stock II 4dc9cc4a691f4ce290f29f3dd2744031.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Given daily prices, maximize profit when you may buy and sell as many times as you like (but hold at most one share). The winning idea: greedily collect every positive day-to-day increase.

## Approaches
- **Greedy sum of upward steps (O(n) time, O(1) space):** whenever tomorrow's price is higher than today's, add the difference to profit. Summing all the "up" segments equals capturing every profitable stretch.

## Best solution
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int days = prices.size();
        int i = 0;
        int profit = 0;

        while (i < days - 1) {
            if (prices[i] < prices[i+1]) {
                profit += prices[i+1] - prices[i];
            }

            ++i;
        }

        return profit;
    }
};
```
Optimal because a single linear pass captures all profit: any long rise decomposes into consecutive small rises, so summing daily gains equals the best multi-transaction result.

## Notes
The insight (from the linked video) is telescoping: for an increasing run a→b→c→d, `d - a = (b-a) + (c-b) + (d-c)`. So buying at every local dip and selling at every local peak is the same as summing each consecutive positive delta — no need to actually track buy/sell points.

## Techniques
[[Greedy Algorithm]]

## Sources
- [[122 Best Time to Buy and Sell Stock II]] raw note — `raw/notes/DSA/DSA/122 Best Time to Buy and Sell Stock II 4dc9cc4a691f4ce290f29f3dd2744031.md`
