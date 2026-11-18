# 125. Valid Palindrome

Time Complexity: O(n)

Space Complexity: O(n) ← because of pass by reference for s in `checkPalindrome` function, way lesser memory is used.

```cpp
class Solution {
public:
    bool checkPalindrome(int l, int r, string &s) {
        if (l >= r) return true;
        if (s[l] != s[r]) return false;
        // TODO: I need to understand why we are returning though, just func
        // call ain't enough?
        return checkPalindrome(l+1, r-1, s);
    }

    bool isPalindrome(string s) {
        string processedString;

        for (char c: s) {
            if (isalnum(c))
                processedString.push_back(tolower(c));
        }

        return checkPalindrome(0, processedString.length() - 1, processedString);
    }
};
```