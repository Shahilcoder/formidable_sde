---
type: source
area: sde
title: 1291 Sequential Digits
aliases: [1291 Sequential Digits, Sequential Digits]
tags: [dsa, arrays, enumeration]
status: draft
source_type: note
author: Shahil Hussain
raw_path: raw/notes/DSA/DSA/1291 Sequential Digits.md
ingested: 2026-07-14
created: 2026-07-14
updated: 2026-07-14
---

## TL;DR
Return every number in `[low, high]` whose digits are strictly consecutive (each digit is one more than the previous, e.g. `123`, `4567`). The whole problem hinges on one observation: there are only **36** such numbers in existence (8 two-digit, 7 three-digit, …, 1 nine-digit), all built from the digits `1-9`. So you don't search the range — you enumerate that tiny fixed catalog and keep the ones that fall in `[low, high]`. Both approaches are therefore **O(1) time and space**. See [[Bounded Solution Space]].

## Approaches
- **Increment digits + sort** — grow a number by appending the next digit (`num = num*10 + d`); when it overflows `high` or `d` passes 9, reset to the next starting digit. Because starting digits are tried in order but each grows to different lengths, the collected numbers come out jumbled, so a final `sort` is needed. O(1) (bounded to ≤36 numbers).
- **Substring of `"123456789"` (cleanest, recommended)** — for each length `2..9`, slide a fixed-width window across the string `"123456789"` and `stoi` each window; keep those in range. **No sort needed**: shorter lengths are generated first, and within a length the starting digit only increases, so output is already ascending. A window slide over a constant string — see [[Sliding Window]].

## Best solution
```cpp
class Solution {
public:
    vector<int> sequentialDigits(int low, int high) {
        string s = "123456789";
        vector<int> result;

        for (int len = 2; len <= 9; len++) {
            for (int i = 0; i + len <= 9; i++) {
                int num = stoi(s.substr(i, len));
                if (num >= low && num <= high)
                    result.push_back(num);
            }
        }
        // already increasing: shorter lengths first, then by starting digit
        return result;
    }
};
```
Optimal because the candidate universe is a fixed 36-element catalog embedded in `"123456789"`, so generation is constant-work, and the natural generation order is exactly ascending — the `sort` that Approach 1 needs disappears.

## Notes
- Digits are restricted to `1-9`: a `0` can never appear, since a run where each digit is prev+1 can't contain `0` (nothing precedes it) and can't start with one.
- Approach 1's reset logic (`d = ++starting; num = d;`) is the fiddly part; Approach 2 sidesteps state entirely by reading substrings out of the constant string.
- Classic interview lesson: when the answer space is provably constant, "brute force" is O(1) — recognize the bound before reaching for anything cleverer.

## Techniques
[[Bounded Solution Space]] · [[Sliding Window]]

## Sources
- [[1291 Sequential Digits]] raw note — `raw/notes/DSA/DSA/1291 Sequential Digits.md`
