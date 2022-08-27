递归三部曲
1. 构建递归函数，确定输入
2. 确定中止条件
3. 单层搜索逻辑，比如
```
for i in range(len(nums)):
    path.append(nums[i])
    backtracking(nums, i + 1)
    pacth.pop()
```

模版如下：
```python
def backtracking(参数):
    if(终止条件):
        存放结果
        return
    for(选择: 本层集合中元素):
        处理节点
        backtracking(路径，选择列表) # 递归
        回溯，撤销结果
```