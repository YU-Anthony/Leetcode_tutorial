`Binary search` 是典型的「减治思想」的应用，核心理论是将搜索区间逐渐缩小，以达到缩减规模的目的。

接下来，我会以[704. Binary Search](https://leetcode.cn/problems/binary-search/)为例，介绍 `Binary Search` 常用的几个模版。

# Template 1
while 结束后并不会收敛出任何元素

适合用在

1. input array 一定包含 target 且 target 只存在一个
2. 希望把 array 内所有的元素都搜寻过
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l, r = 0, len(nums) - 1
        
        while l <= r:
            m = (l + r) // 2
            if nums[m] < target:
                l = m + 1
            elif nums[m] > target:
                r = m - 1
            elif nums[m] == target:
                return m
        return -1
```
- Initial Condition: `left = 0, right = length - 1`
- Termination: `left > right`
- Searching Left: `right = mid - 1`
- Searching Right: `left = mid + 1`
- 搜寻区间：`左闭右闭`

# Template 2
while 结束后会收敛得到一个元素，代表`binary seach`过程中，区间至少会有两个元素，搜寻结束后必须得处理剩下的那一个元素。
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l, r = 0, len(nums)
        
        while l < r:
            m = (r + l) // 2
            if nums[m] < target:
                l = m + 1
            elif nums[m] > target:
                r = m
            elif nums[m] == target:
                return m
        return -1
```
- Initial Condition: `left = 0, right = length`
- Termination: `left == right`
- Searching Left: `right = mid`
- Searching Right: `left = mid + 1`
- 搜寻区间：`左闭右闭`

Here are three different templates for solving binary search problems:

Template #1: Search for a target value in a sorted array
```python
def binarySearch(nums, target):
    left, right = 0, len(nums) - 1
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```
Template #2: Search for the first occurrence of a target value in a sorted array
```python
def binarySearchFirst(nums, target):
    left, right = 0, len(nums) - 1
    while left < right:
        mid = (left + right) // 2
        if nums[mid] < target:
            left = mid + 1
        else:
            right = mid
    return left if nums[left] == target else -1
```
Template #3: Search for the last occurrence of a target value in a sorted array
```python
def binarySearchLast(nums, target):
    left, right = 0, len(nums) - 1
    while left < right:
        mid = (left + right + 1) // 2
        if nums[mid] > target:
            right = mid - 1
        else:
            left = mid
    return left if nums[left] == target else -1
```
The differences between the three templates:

Template #1 is for searching for a target value in a sorted array. It returns the index of the target value if it exists, or -1 if it does not exist.

Template #2 is for searching for the first occurrence of a target value in a sorted array. It returns the index of the first occurrence of the target value if it exists, or -1 if it does not exist.

Template #3 is for searching for the last occurrence of a target value in a sorted array. It returns the index of the last occurrence of the target value if it exists, or -1 if it does not exist.


# 常见题目
| Problems                                                                                                     | Rating                                                                                                                                                                    | Level|Comment|
| ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---- | ---- |
| [704.Binary Search](https://leetcode.cn/problems/binary-search/) | 🌟🌟🌟🌟🌟 | <font color=green> Easy </font>|入门题目|
|[4.Median of Two Sorted Arrays](https://leetcode.cn/problems/median-of-two-sorted-arrays/)|🌟🌟🌟🌟🌟| <font color=red> Hard </font>|应该算是 Binary Search 最难的题目，`Amazon`,`Bytedance`,`Apple`,`Microsoft`|
|[875.Koko Eating Bananas](https://leetcode.cn/problems/koko-eating-bananas/)|| <font color=yellow> `Medium` </font>||
|[33.Search in Rotated Sorted Array](https://leetcode.cn/problems/search-in-rotated-sorted-array/)|🌟🌟🌟🌟🌟| <font color=yellow> `Medium` </font>|`Amazon`, `Microsoft`, `Facebook`, `Bytedance`|
|[153.Find Minimum in Rotated Sorted Array](https://leetcode.cn/problems/find-minimum-in-rotated-sorted-array/)|🌟🌟🌟🌟| <font color=yellow> `Medium` </font>||
|[981.Time Based Key-Value Store](https://leetcode.cn/problems/time-based-key-value-store/)|🌟🌟🌟🌟| <font color=yellow> `Medium` </font>|`Amazon`,`Google`|