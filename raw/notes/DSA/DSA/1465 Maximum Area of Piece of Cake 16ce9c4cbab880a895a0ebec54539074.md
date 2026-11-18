# 1465. Maximum Area of Piece of Cake

(MY OWN First Submit and Accept at first shot)

Sorting then Greedy approach:

Sort the `horizontalCuts` and `verticalCuts` arrays as they are not sorted.

append `h` and `w` to the respective arrays, because they are ALSO part of the cake, the ending portion of the cake. Need to include them too.

NOW we need to find the max horizontal continuous length (`max_h`), and in same way max vertical continuous length (`max_w`), with no cuts coming in between.

return

```cpp
(max_h * max_w) % 1000000007
```

Doing the modulo for whatever reason the question said to.

```cpp
class Solution {
public:
    int maxArea(int h, int w, vector<int>& horizontalCuts, vector<int>& verticalCuts) {
        sort(horizontalCuts.begin(), horizontalCuts.end());
        sort(verticalCuts.begin(), verticalCuts.end());

        horizontalCuts.push_back(h);
        verticalCuts.push_back(w);

				// Initialize the MAX as the 0th side of cake to the very first CUT.
        long max_h = horizontalCuts[0];
        long max_w = verticalCuts[0];

        for (int i=1, s=horizontalCuts.size(); i<s; ++i)
            max_h = max(max_h, (long)(horizontalCuts[i] - horizontalCuts[i-1]));

        for (int i=1, s=verticalCuts.size(); i<s; ++i)
            max_w = max(max_w, (long)(verticalCuts[i] - verticalCuts[i-1]));

        return (max_h * max_w) % (1000000007);
    }
};
```