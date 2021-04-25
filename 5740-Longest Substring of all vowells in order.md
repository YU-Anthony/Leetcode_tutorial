## Problem
A string is considered beautiful if it satisfies the following conditions:
- Each of the 5 English vowels ('a', 'e', 'i', 'o', 'u') must appear at least once in it.
- The letters must be sorted in alphabetical order (i.e. all 'a's before 'e's, all 'e's before 'i's, etc.).
For example, strings "aeiou" and "aaaaaaeiiiioou" are considered beautiful, but "uaeio", "aeoiu", and "aaaeeeooo" are not beautiful.

Given a string word consisting of English vowels, return the length of the longest beautiful substring of word. If no such substring exists, return 0.

A **substring** is a contiguous sequence of characters in a string.

## Example
```bash
Input: word = "aeiaaioaaaaeiiiiouuuooaauuaeiu"
Output: 13
Explanation: The longest beautiful substring in word is "aaaaeiiiiouuu" of length 13.
```

## Solution
将 a,e,i,o,u 看成 5 个状态。
当我们在遍历字符串的每个字符时，都会处于其中的一个状态。如果当前在 u 状态，那么就可以对答案进行更新。

```python
class Solution:

    TRANSIT = {
        ("a", "e"), ("e", "i"), ("i", "o"), ("o", "u"),
        ("a", "a"), ("e", "e"), ("i", "i"), ("o", "o"), ("u", "u"),
        ("x", "a"), ("e", "a"), ("i", "a"), ("o", "a"), ("u", "a"),
    }
    
    def longestBeautifulSubstring(self, word: str) -> int:
        cur, ans = 0, 0
        status = "x"
        
        for ch in word:
            if (status, ch) in Solution.TRANSIT:
                if status != "a" and ch == "a":
                    cur = 1
                else:
                    cur = cur + 1
                status = ch
            else:
                cur = 0
                status = "x"
            if status == "u":
                ans = max(ans, cur)

        return ans
```