> hard
# Problem
Words Concatenation (hard)

Given a string and a list of words, find all the starting indices of substrings in the given string that are a concatenation of all the given words exactly once without any overlapping of words. It is given that all words are of the same length.

Example 1
```
Input: String="catfoxcat", Words=["cat", "fox"]
Output: [0, 3]
Explanation: The two substring containing both the words are "catfox" & "foxcat".
```

Example 2
```
Input: String="catcatfoxfox", Words=["cat", "fox"]
Output: [3]
Explanation: The only substring containing both the words is "catfox".
```
# Answer
```python
from collections import defaultdict
def find_word_concatenation(str1, words):
    pattern = defaultdict(int)
    for word in words:
        pattern[word] += 1
    window = defaultdict(int)
    l, matched = 0, 0
    word_cnt = len(words)
    word_len = len(words[0])
    ans = []
    
    for i in range((len(str1) - word_cnt * word_len) + 1):
        seen = defaultdict(int)
        for j in range(word_cnt):
            next_word_idx = i + j * word_len
            word = str1[next_word_idx:next_word_idx + word_len]
            if word not in pattern:
                break
            seen[word] += 1
            if seen[word] > pattern[word]:
                break
            if j + 1 == word_cnt:
                ans.append(i)
    return ans

print(find_word_concatenation("catcatfoxfox", ["cat", "fox"]))
```
Time Complexity
- The time complexity of the above algorithm will be O(N * M * Len) where ‘N’ is the number of characters in the given string, ‘M’ is the total number of words, and ‘Len’ is the length of a word.

Space Complexity#
- The space complexity of the algorithm is O(M) since at most, we will be storing all the words in the two HashMaps. In the worst case, we also need O(N) space for the resulting list. So, the overall space complexity of the algorithm will be O(M+N).