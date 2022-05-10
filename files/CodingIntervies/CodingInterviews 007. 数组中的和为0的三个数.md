# Question
给定一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a ，b ，c ，使得 a + b + c = 0 ？请找出所有和为 0 且 不重复 的三元组。

Example 1:
```bash
输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]
```

Example 2:
```bash
输入：nums = []
输出：[]
```

Example 3:
```bash
输入：nums = [0]
输出：[]
```

Answer:

Actually, this is a variation of question `Two Sum`. For the question of Two Sum, we used double pointers and track the sum of values of two pointers with the target value. In this problem, we can still use the method of `Double Pointers`, but need to add a `for-loop` at the outermost layer. What's more, we need to be careful of the duplicate values.

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        res=[]
        for i in range(len(nums)-2):
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            target_=-nums[i]
            l,r=i+1,len(nums)-1
            while l<r:
                sum_=nums[l]+nums[r]
                if target_==sum_:
                    res.append([nums[i],nums[l],nums[r]])
                    while l<r:
                        l+=1
                        if nums[l]!=nums[l-1]:
                            break
                    while l<r:
                        r-=1
                        if nums[r]!=nums[r+1]:
                            break
                elif target_<sum_:
                    r-=1
                else:
                    l+=1
        return res

```
