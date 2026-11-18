# 48. Rotate Image

Mafizuddin and My Approach:

Time Complexity: O(n^2)

Space Complexity: O(1)

Traverse through the upper (or lower) triangle of `\` diagonal and swap them with their mirror opposites w.r.t `\` .

Reverse each and every row of the Matrix.

Upper triangle

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int rows = matrix.size();
        int cols = matrix[0].size();

        // traverse through upper triangle of \ diagonal
        // swap the mirror opposite elements
        for (int i=0; i<rows; ++i) {
            for (int j=i+1; j<cols; ++j)
                swap(matrix[i][j], matrix[j][i]);
        }

        // reverse each and every row
        for (auto &row: matrix) reverse(row.begin(), row.end());
    }
};
```

Lower triangle

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int rows = matrix.size();
        int cols = matrix[0].size();

        // traverse through lower triangle of \ diagonal
        // swap the mirror opposite elements
        for (int i=0; i<rows; ++i) {
            for (int j=0; j<i; ++j)
                swap(matrix[i][j], matrix[j][i]);
        }

        // reverse each and every row
        for (auto &row: matrix) reverse(row.begin(), row.end());
    }
};
```