# 1423. Maximum points obtain from card

Sliding window approach:

Time Complexity: O(k), k → no. of cards to pick.

Space Complexity: O(1)

Watch Neetcode’s video.

start with a window starting from index `l=0` till `r = n - k`, hence leaving `k` elements at end. Find the sum of those `k` elements at end. For now take it as `max_sum`.

Now just subtract `arr[l]`  and add `arr[r]`  to current sum, also increment `l` and `r`  by 1. Hence making the window slide, while also updating the resulting sum outside of the window.

And yes, Keep checking if resulting sum should be our `max_sum`.

```cpp
class Solution {
public:
    int maxScore(vector<int>& cardPoints, int k) {
        int size = cardPoints.size();

        int l = 0;
        int r = size - k; // Note: we will treat it as [l, r)

        int max_sum = 0;

        // runs about k times
        for (int i=r; i<size; ++i) max_sum += cardPoints[i];

        int totalSum = max_sum;
        while (r < size) {
            totalSum = totalSum - cardPoints[r++] + cardPoints[l++];
            max_sum = max(totalSum, max_sum);
        }

        return max_sum;
    }
};
```