> hard
# Problem
Smallest Window containing Substring (hard)

Given a string and a pattern, find the smallest substring in the given string which has all the character occurrences of the given pattern.

Example 1:
```
Input: String="aabdec", Pattern="abc"
Output: "abdec"
Explanation: The smallest substring having all characters of the pattern is "abdec"
```

Example 2:
```
Input: String="aabdec", Pattern="abac"
Output: "aabdec"
Explanation: The smallest substring having all character occurrences of the pattern is "aabdec"
```

Example 3:
```
Input: String="abdbca", Pattern="abc"
Output: "bca"
Explanation: The smallest substring having all characters of the pattern is "bca".
```
# Answer
```python
from collections import defaultdict
def find_substring(str1, pattern):
    res_pattern = defaultdict(int)
    window = defaultdict(int)
    for c in pattern:
        res_pattern[c] += 1
    l, start, minLen = 0, 0, float("inf")
    matched = 0
    for r, val in enumerate(str1):
        window[val] += 1
        if val in res_pattern and window[val] == res_pattern[val]:
            matched += 1
        
        while matched == len(res_pattern):
            if minLen > r - l + 1:
                start = l
                minLen = r - l + 1
            window[str1[l]] -= 1
            if str1[l] in res_pattern and window[str1[l]] != res_pattern[str1[l]]:
                matched -= 1
            l += 1
            
    return str1[start: start + minLen] if minLen != float("inf") else ""
print(find_substring("adcad", "abc"))
```

Time Complexity
- The time complexity of the above algorithm will be O(N + M) where ‘N’ and ‘M’ are the number of characters in the input string and the pattern respectively.

Space Complexity
- The space complexity of the algorithm is O(M) since in the worst case, the whole pattern can have distinct characters which will go into the HashMap. In the worst case, we also need O(N) space for the resulting substring, which will happen when the input string is a permutation of the pattern.