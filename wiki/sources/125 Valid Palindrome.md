---
type: source
area: sde
title: 125 Valid Palindrome
aliases: [125 Valid Palindrome, Valid Palindrome]
tags: [dsa, string, two-pointer]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/125 Valid Palindrome 1cde9c4cbab880b0b055cb84f7f08d34.md
ingested: 2026-07-12
created: 2026-07-12
updated: 2026-07-12
---

## TL;DR
Decide whether a string is a palindrome considering only alphanumeric characters and ignoring case. The winning idea: normalize to lowercase alphanumerics, then compare from both ends inward with two pointers.

## Approaches
- **Filter + recursive two-pointer check (O(n) time, O(n) space):** first build a cleaned string of lowercased alphanumeric characters, then recursively compare the outermost characters and move inward (`l`, `r`) until the pointers cross. The O(n) extra space is the cleaned string.

## Best solution
```cpp
class Solution {
public:
    bool checkPalindrome(int l, int r, string &s) {
        if (l >= r) return true;
        if (s[l] != s[r]) return false;
        return checkPalindrome(l + 1, r - 1, s);
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
Optimal on time (single linear scan of the string). Passing `s` by reference avoids copying the string on every recursive frame. An iterative two-pointer loop would drop the O(n) cleaned-string allocation to O(1) if you skip non-alphanumerics in place.

## Notes
> [!note] Claude's addition
> **Why must the recursive call be `return`ed?** The helper returns `bool`; a bare recursive call discards the sub-result and the function falls through, so the answer from deeper frames never propagates. `return`ing the call threads the boolean back up. (An iterative two-pointer loop sidesteps this and is the more idiomatic solution.)

## Techniques
[[Two Pointer Technique]]

## Sources
- [[125 Valid Palindrome]] raw note — `raw/notes/DSA/DSA/125 Valid Palindrome 1cde9c4cbab880b0b055cb84f7f08d34.md`
