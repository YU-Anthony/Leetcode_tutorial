```python
def twoSum(nums,target):
  hashmap = {}
  for index, num in enumerate(nums):
    hashmap[num]=index
    
  for i,num in enumerate(nums):
    j=hashmap.get(target-num)
    if j is not None and i!=j:
      return [i,j]
```
