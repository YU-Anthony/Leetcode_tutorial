# Problems
给定一个正整数数组 nums和整数 k ，请找出该数组内乘积小于 k 的连续的子数组的个数。

Example 1
```
输入: nums = [10,5,2,6], k = 100
输出: 8
解释: 8 个乘积小于 100 的子数组分别为: [10], [5], [2], [6], [10,5], [5,2], [2,6], [5,2,6]。
需要注意的是 [10,5,2] 并不是乘积小于100的子数组。
```

Example 2
```
输入: nums = [1,2,3], k = 0
输出: 0
```

# Answer
这道题其实也能用 sliding window 来解，但是由于不是求最短或最长连续子数组的长度，不能直接生搬原来的模版。我们注意这里是求连续子数组的个数，所以我们可以累加滑动窗口内数组的个数。
而滑动窗口每次发生变化都会新增当前滑动窗口长度的数组。
```python
class Solution:
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
        left, ret =0, 0
        total = 1

        for right, val in enumerate(nums):
            total *= val
            while left <= right and total >= k:
                total /= nums[left]
                left += 1
            if left <= right:
                ret += right-left+1
        return ret
```

TC: O(n) 其中 n 是数组 nums 的长度。两个端点 i 和 j 的增加次数都不超过 n。
SC: O(1)