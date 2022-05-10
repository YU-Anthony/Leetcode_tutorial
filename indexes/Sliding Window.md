> 此模版参考 清风Python 

双指针的解题思路一般分为三类：
- 首尾指针：范围查找，比如二分搜索等
- 滑动窗口：指针在数组同一方向，根据条件移动左右指针，用于获取范围和等
- 快慢指针：多用于链表计算，判断是否有环。

今天介绍的就是`滑动窗口`的模版。一般滑动窗口的题目中都会有明确的`连续子数组`、`连续子串`等关键词，可能还会附带`最大`、`最小`的限定词进行补充。
遇到这类问题可分为以下几步：
1. 初始化窗口左边为0，右边界可以为0，也可以根据题意固定大小
2. 初始化一个 ret 的返回值，可以设置为最大或者最小
3. 窗口的大小需要根据题目条件进行调整：
- `最大连续`...尽量扩张右边界，直到不满足题意再收缩左边界
- `最小连续`...尽量缩小左边界，直到不满足题意再扩大右边界
4. 在执行3的过程中，不断与 ret 进行比较
5. 最终返回 ret 的结果

具体模版如下：
```
 初始化左边界 l = 0
 初始化返回值 ret = 最小值 or 最大值
 for r(右边界) in 可迭代对象:
    更新窗口内部信息
    while 根据题意进行调整:
        比较并更新 ret(收缩场景时)
        扩张或收缩窗口大小
    比较并更新 ret(扩张场景时)
 return ret
```

常见题目：
| Problems                                                                                                     | Answer                                                                                                                                                                    | Level|
| ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---- | 
| [剑指 Offer II 008. 和大于等于 target 的最短子数组](https://leetcode.cn/problems/2VG8Kg/) | [Link](https://github.com/YU-Anthony/Leetcode_tutorial/blob/main/CodingIntervies/CodingInterviews%20008.%20%E5%92%8C%E5%A4%A7%E4%BA%8E%E7%AD%89%E4%BA%8E%20target%20%E7%9A%84%E6%9C%80%E7%9F%AD%E5%AD%90%E6%95%B0%E7%BB%84.md) | <font color=yellow> `Medium` </font>|
|[3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)|[Link](https://github.com/YU-Anthony/Leetcode_tutorial/blob/main/files/problems1_500/3.%20Longest%20Substring%20Without%20Repeating%20Characters.md)| <font color=yellow> `Medium` </font>|
