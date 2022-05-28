# Problems
给定一个整数数组和一个整数 k ，请找到该数组中和为 k 的连续子数组的个数。

Example 1
```bash
输入:nums = [1,1,1], k = 2
输出: 2
解释: 此题 [1,1] 与 [1,1] 为两种不同的情况
```

Example 2
```bash
输入:nums = [1,2,3], k = 3
输出: 2
```

Hints:
- 1 <= nums.length <= 2 * 104
- -1000 <= nums[i] <= 1000
- -107 <= k <= 107

# Answer
这道题乍一看到`连续子数组`的关键词，我兴致勃勃的觉得可以用`sliding window`的方法来解，于是写了下面的答案：
```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        left, res = 0, 0
        total = 0
        for right, val in enumerate(nums):
            total += val
            while left <= right and total > k:
                total -= nums[left]
                left += 1
            if left <= right and total == k:
                res += 1
        return res
```
这个解法在处理两个Examples确实能输出正确的答案，但是我们忽略了一点,题意中的数组值是允许出现负值的，而滑动窗口只能处理所有值都为正的情况。

具体分析：滑动窗口向右移动右指针以增加值，向右移动左指针以减小值，但当出现负数的时候，**每一次加入值不一定会增加总体的大小，每一次减去值不一定减小总体的大小**，因此`滑动窗口`的方法在这里不可取！

下面是正确解法：

⚠️前方预警：有点绕

题目让我们求连续子数组的和为`k`的个数。在前缀
以Example1为例, 子数组[i+1,i+2]（这里是前闭后闭）的和其实相当于 prefix_arr[i+2]-prefix_arr[i] 的差值。那么题意中找到子数组的和为k的子数组个数其实就是让我们找 prefix_arr[j]-prefix_arr[i] == k 的子数组的个数，换个角度思考就是找 prefix_arr[i]==prefix_arr[j]-k 的个数，这里的 j 可以为 i+2 也可能为任何值。
```bash
              i i+1 i+2
origin_arr    1  1  1
prefix_arr    1  2  3
```
再换个角度思考，被减数-减数=k， 求k的个数及求减数(被减数-k)的个数，

在下面的例子中，被减数是我们每一步更新的 pre_sum，减数是历史记录里的(被减数-k)
```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        ret, pre_sum = 0, 0
        pre_dict = {0:1}
        for i in nums:
            pre_sum += i
            ret += pre_dict.get(pre_sum-k,0)
            pre_dict[pre_sum] = pre_dict.get(pre_sum,0)+1
        return ret
```
