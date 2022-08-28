> 参考资料：
> 1. https://programmercarl.com/%E5%9B%9E%E6%BA%AF%E6%80%BB%E7%BB%93.html#%E8%A7%A3%E6%95%B0%E7%8B%AC%E9%97%AE%E9%A2%98

递归三部曲
1. 构建递归函数，确定输入和返回值
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
![](https://code-thinking-1253855093.file.myqcloud.com/pics/20211030124742.png)
# Problems
1. 子集
- [78. Subsets](https://leetcode.com/problems/subsets/)
- [90. Subsets II](https://leetcode.com/problems/subsets-ii/)
2. 组合
- [77. Combinations](https://leetcode.com/problems/combinations/)
- [39. Combination Sum](https://leetcode.com/problems/combination-sum/)
- [40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)
- [216. Combination Sum III](https://leetcode.com/problems/combination-sum-iii/)
- [17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)


# 时间、空间复杂度分析
## 子集问题分析：
- 时间复杂度：O(2^n)，因为每一个元素的状态无外乎取与不取，所以时间复杂度为O(2^n)
- 空间复杂度：O(n)，递归深度为n，所以系统栈所用空间为O(n)，每一层递归所用的空间都是常数级别，注意代码里的result和path都是全局变量，就算是放在参数里，传的也是引用，并不会新申请内存空间，最终空间复杂度为O(n)
## 排列问题分析：
- 时间复杂度：O(n!)，这个可以从排列的树形图中很明显发现，每一层节点为n，第二层每一个分支都延伸了n-1个分支，再往下又是n-2个分支，所以一直到叶子节点一共就是 n * n-1 * n-2 * ..... 1 = n!。
- 空间复杂度：O(n)，和子集问题同理。
## 组合问题分析：
- 时间复杂度：O(2^n)，组合问题其实就是一种子集的问题，所以组合问题最坏的情况，也不会超过子集问题的时间复杂度。
- 空间复杂度：O(n)，和子集问题同理。
## N皇后问题分析：
- 时间复杂度：O(n!) ，其实如果看树形图的话，直觉上是O(n^n)，但皇后之间不能见面所以在搜索的过程中是有剪枝的，最差也就是O（n!），n!表示n * (n-1) * .... * 1。
- 空间复杂度：O(n)，和子集问题同理。
## 解数独问题分析：
- 时间复杂度：O(9^m) , m是'.'的数目。
- 空间复杂度：O(n^2)，递归的深度是n^2