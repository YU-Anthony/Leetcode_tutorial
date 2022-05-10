# Question
给定一个含有 n 个正整数的数组和一个正整数 target 。

找出该数组中满足其和 ≥ target 的长度最小的 连续子数组 [numsl, numsl+1, ..., numsr-1, numsr] ，并返回其长度。如果不存在符合条件的子数组，返回 0 。

Example 1:
```
输入：target = 7, nums = [2,3,1,2,4,3]
输出：2
解释：子数组 [4,3] 是该条件下的长度最小的子数组。
```

Example 2:
```
输入：target = 4, nums = [1,4,4]
输出：1
```

Example 3:
```
输入：target = 11, nums = [1,1,1,1,1,1,1,1]
输出：0
```

Answer:
Solution 1: Prefix sum + binary search
At first, we need to create the prefix sum `res`. For each index in `nums`, we need to find the least index `bound` to make `res[bound]-res[i] >= target`. So the range of 
the shorest continus subarray is `bound-i+1`.
```
res=[0]
for i in nums:
    res.append(i+res[-1])
ans=inf
for i in range(len(nums)):
    l,r=i,len(nums)
    while l<r:
        mid=
        if res[mid+1]-res[i]>=target:
            r=mid
            ans=min(ans,mid-i+1)
        else:
            l=mid+1
return 0 if ans==inf else ans
```

Solution 2: Sliding window
Actuallt this is also `double pointers` solution. We set a variable to record the sum of subarrays. If the current sum >= target, we shrink the subarray by increasing its left bound until the sum less than target.
In the last step, we could get the least length of subarrays based on the current index.

```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        left=total=0
        ret=inf
        for right in range(len(nums)):
            total+=nums[right]
            while total>=target:
                ret=min(ret,right-left+1)
                total-=nums[left]
                left+=1
        return 0 if ret==inf else ret
```
