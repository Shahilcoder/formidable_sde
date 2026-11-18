# 122. Best Time to Buy and Sell Stock II

Greedy approach:

https://youtu.be/3gtcRtvDCpA?si=sAyLzr5Rt35llpxK

Think of the numbers in terms of graph, or height levels

for some increase in height abcd : d-a = b-a + c-b + d-c

Time Complexity: O(n)

Space Complexity: O(1)

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int days = prices.size();
        int i = 0;
        int profit = 0;

        while(i < days - 1) {
            if (prices[i] < prices[i+1]) {
                profit += prices[i+1] - prices[i];
            }

            ++i;
        }

        return profit;
    }
};
```