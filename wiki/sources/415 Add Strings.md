---
type: source
area: sde
title: 415 Add Strings
aliases: [415 Add Strings, Add Strings]
tags: [dsa, string, math]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/415 Add Strings 10de9c4cbab880cca44ce661a18cad29.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Add two non-negative integers given as strings, without converting them to numbers. Simulate grade-school addition digit by digit from the least significant end, tracking a carry, and reverse the accumulated result at the end.

## Approaches
- **Digit-by-digit addition with carry (optimal)** — walk from the last character of each string inward, summing paired digits plus carry; once the shorter string is exhausted, continue over the longer string's remaining digits with the running carry; push a final carry digit if any, then reverse. O(n) time and O(n) space where n is the length of the longer string.

## Best solution
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
Optimal: single linear scan of the digits with O(1) arithmetic per digit; no big-integer type or overflow risk.

## Notes
- `res` is built least-significant-first, so the final `reverse` restores normal order.
- The second loop reuses the shared index `i` to continue over the longer string's leftover digits.

## Techniques
(Standalone — no technique page.)

## Sources
- [[415 Add Strings]] raw note — see `raw_path` above.
