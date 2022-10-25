# Problem
> hard

Given a string, find the length of the longest substring, which has all distinct characters.

Example 1:
```
Input: String="aabccbb"
Output: 3
Explanation: The longest substring with distinct characters is "abc".
```

Example 2
```
Input: String="abbbb"
Output: 2
Explanation: The longest substring with distinct characters is "ab".
```

Example 3
```
Input: String="abccde"
Output: 3
Explanation: Longest substrings with distinct characters are "abc" & "cde".
```
# Answer
This problem follows the Sliding Window pattern, and we can use a similar dynamic sliding window strategy as discussed in Longest Substring with K Distinct Characters. We can use a HashMap to remember the last index of each character we have processed. Whenever we get a duplicate character, we will shrink our sliding window to ensure that we always have distinct characters in the sliding window.

官方答案：
```python
def non_repeat_substring(str1):
  window_start = 0
  max_length = 0
  char_index_map = {}

  # try to extend the range [windowStart, windowEnd]
  for window_end in range(len(str1)):
    right_char = str1[window_end]
    # if the map already contains the 'right_char', shrink the window from the beginning so that
    # we have only one occurrence of 'right_char'
    if right_char in char_index_map:
      # this is tricky; in the current window, we will not have any 'right_char' after its previous index
      # and if 'window_start' is already ahead of the last index of 'right_char', we'll keep 'window_start'
      window_start = max(window_start, char_index_map[right_char] + 1)
    # insert the 'right_char' into the map
    char_index_map[right_char] = window_end
    # remember the maximum length so far
    max_length = max(max_length, window_end - window_start + 1)
  return max_length


def main():
  print("Length of the longest substring: " + str(non_repeat_substring("aabccbb")))
  print("Length of the longest substring: " + str(non_repeat_substring("abbbb")))
  print("Length of the longest substring: " + str(non_repeat_substring("abccde")))


main()
```
- TC: O(N)
- SC: O(K), K is the number of distinct characters

自己的答案：
```python
from collections import defaultdict
def non_repeat_substring(str):
  # TODO: Write your code here
  res = defaultdict(int)
  l, ans = 0, 0
  for r, val in enumerate(str):
    if val in res:
      l = max(l, res[val] + 1)
    res[val] = r
    ans = max(ans, r - l + 1)
  return ans
```