## Question
Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range [-2^31^, 2^31^ - 1], then return 0.

**Assume the environment does not allow you to store 64-bit integers (signed or unsigned)**.

## Example
```bash
Input: x = 123
Output: 321

Input: x = -123
Output: -321
```

## Solution
⚠️ First calculate the result and then judge the range of number
```python
class Solution(object):
    def reverse(self, x):
        result = 0
        new_x = abs(x)

        while(new_x!=0):
            temp = new_x%10
            result=result*10+temp 
            if result > 2**31-1:
                return 0
            new_x //=10
        return result if x>0 else -result
```
Runtime: 20 ms