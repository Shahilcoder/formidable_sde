# 415. Add Strings

Time Complexity: O(n) where n is length of the greatest string

Space Complexity: O(n) where n is length of greatest string

```cpp
class Solution {
public:
    string addStrings(string num1, string num2) {
        int len1 = num1.length();
        int len2 = num2.length();

        int len = min(len1, len2);
        string res;

        int carry = 0;
        int i = 1;
        
        while (i <= len) {
            int last1 = *(num1.end() - i) - '0';
            int last2 = *(num2.end() - i) - '0';

            int sum = last1 + last2 + carry;
            carry = sum / 10;
            sum = sum % 10;

            res.push_back(sum + '0');
            i++;
        }

        string target = len1 > len2 ? num1 : num2;
        len = target.length();

        while (i <= len) {
            int last = *(target.end() - i) - '0';
            int sum = last + carry;
            carry = sum / 10;
            sum = sum % 10;

            res.push_back(sum + '0');
            i++;
        }

        if (carry) res.push_back(carry + '0');

        reverse(res.begin(), res.end());

        return res;
    }
};
```