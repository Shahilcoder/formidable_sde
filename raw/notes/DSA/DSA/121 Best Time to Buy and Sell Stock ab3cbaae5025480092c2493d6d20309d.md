# 121. Best Time to Buy and Sell Stock

Rather than focusing on buy the stock at min price first, focus at what price you are selling first then find minimum buy price from previous days

OR, while traversing the array dig in to minimum value progressively, and find if the difference between prices[i] and minimum is giving more profit, then store it.

Time complexity: O(n)

Space complexity: O(1)

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