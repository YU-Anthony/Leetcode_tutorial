> hard
# Problem
Given a string with lowercase letters only, if you are allowed to replace no more than k letters with any letter, find the length of the longest substring having the same letters after replacement.

Example 1
```
Input: String="aabccbb", k=2
Output: 5
Explanation: Replace the two 'c' with 'b' to have the longest repeating substring "bbbbb".
```

Example 2
```
Input: String="abbcb", k=1
Output: 4
Explanation: Replace the 'c' with 'b' to have the longest repeating substring "bbbb".
```

Example 3
```
Input: String="abccde", k=1
Output: 3
Explanation: Replace the 'b' or 'd' with 'c' to have the longest repeating substring "ccc".
```

# Answer
We could use a `HashMap` to store the frequency of each letter
- Iterate through the string to add one letter to the window
- Keep track of the count of maximum repeating letter `maxRepeatLetterCount`in any window
    - If windowLength - maxRepeatLetterCount > k, we shrink the window 
- Keep update the windowLength
## 自己的答案
```python
from collections import defaultdict
def length_of_longest_substring(str1, k):
  # TODO: Write your code here
  res = defaultdict(int)
  l, ans = 0, 0
  for r, val in enumerate(str1):
    res[val] += 1
    max_freq = max(res.values())
    while r - l + 1 - max_freq > k:
      res[str1[l]] -= 1
      l += 1
    ans = max(ans, r - l + 1)
  return ans
```



## 官方答案

This problem follows the Sliding Window pattern, and we can use a similar dynamic sliding window strategy as discussed in Longest Substring with Distinct Characters. We can use a HashMap to count the frequency of each letter.

- We will iterate through the string to add one letter at a time in the window.
- We will also keep track of the count of the maximum repeating letter in any window (let’s call it maxRepeatLetterCount).
- So, at any time, we know that we do have a window with one letter repeating maxRepeatLetterCount times; this means we should try to replace the remaining letters.
        - If the remaining letters are less than or equal to k, we can replace them all.
        - If we have more than k remaining letters, we should shrink the window as we cannot replace more than k letters.

While shrinking the window, we don’t need to update maxRepeatLetterCount. Since we are only interested in the longest valid substring, our sliding windows do not have to shrink, even if a window may cover an invalid substring. . We only expand the window when the frequency of the newly added character exceeds the historical maximum frequency (from a previous window that included a valid substring). In other words, we do not need to know the exact maximum count of the current window. The only thing we need to know is whether the maximum count exceeds the historical maximum count, and that can only happen because of the newly added char.

```python
def length_of_longest_substring(str1, k):
  window_start, max_length, max_repeat_letter_count = 0, 0, 0
  frequency_map = {}

  # Try to extend the range [window_start, window_end]
  for window_end in range(len(str1)):
    right_char = str1[window_end]
    if right_char not in frequency_map:
      frequency_map[right_char] = 0
    frequency_map[right_char] += 1
    
    # we don't need to place the maxRepeatLetterCount under the below 'if', see the 
    # explanation in the 'Solution' section above.
    max_repeat_letter_count = max(
      max_repeat_letter_count, frequency_map[right_char])

    # Current window size is from window_start to window_end, overall we have a letter which is
    # repeating 'max_repeat_letter_count' times, this means we can have a window which has one letter
    # repeating 'max_repeat_letter_count' times and the remaining letters we should replace.
    # if the remaining letters are more than 'k', it is the time to shrink the window as we
    # are not allowed to replace more than 'k' letters
    if (window_end - window_start + 1 - max_repeat_letter_count) > k:
      left_char = str1[window_start]
      frequency_map[left_char] -= 1
      window_start += 1

    max_length = max(max_length, window_end - window_start + 1)
  return max_length


def main():
  print(length_of_longest_substring("aabccbb", 2))
  print(length_of_longest_substring("abbcb", 1))
  print(length_of_longest_substring("abccde", 1))


main()
```
- TC: The above algorithm’s time complexity will be O(N), where ‘N’ is the number of letters in the input string.

- SC: As we expect only the lower case letters in the input string, we can conclude that the space complexity will be O(26) to store each letter’s frequency in the HashMap, which is asymptotically equal to O(1).