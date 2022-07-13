> 参考资料：<br>
> [【刷题总结】堆系列问题](https://blog.csdn.net/github_36955602/article/details/117666646)
# 一. 堆的基本性质
## 1. 堆的定义
堆是一种特别的二叉树，具有两个特性
- 完全二叉树
- 每个节点的值都必须「大于等于」或者「小于等于」其孩子节点的值
## 2. 堆的特性
- 插入元素: O(logn)
- 删除元素: O(logn)
- 获取堆中的「最大值」或「最小值」: O(1)
# 3. 堆的分类
 最大堆：堆中每一个节点的值都「大于等于」其孩子节点的值

 最小堆：堆中每一个节点的值都「小于等于」其孩子节点的值
 > 注意 Python 语言中只有最小堆是内置的，如果想要实现「最大堆」，我们可以将所有元素取负再存入最小堆中，这样对堆顶元素取负仍可以得到最大值。

 # 二. 堆的应用
 ### 找前 K 大元素
 解法1
 ```
1. 创建一个「最大堆」；
2. 将所有元素都加到「最大堆」中；
3. 通过边删除边遍历方法，将堆顶元素删除，并将它保存到结果集 T 中；
4. 重复3步骤 K 次，直到取出前K个最大的元素；
 ```
 解法2
 ```
1.创建一个大小为 K 的「最小堆」；
2.依次将元素添加到「最小堆」中；
3.当「最小堆」的元素个数达到 K 时，将当前元素与堆顶元素进行对比：
4.如果当前元素小于堆顶元素，则放弃当前元素，继续进行下一个元素；
5.如果当前元素大于堆顶元素，则删除堆顶元素，将当前元素加入到「最小堆」中。
6.重复步骤 2 和步骤 3，直到所有元素遍历完毕。
 ```
 > [973.K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)<br>
 > [373.Find K Pairs with Smallest Sums](https://leetcode.com/problems/find-k-pairs-with-smallest-sums/)

 > [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)

`最小堆`, `bucket sort`。这道题要求出现频率前k高的元素，我们可以用 `hashtable`来存各个元素的频数，然后用大小为k的「最小堆」去存各个元素，最后堆内即为较大的 k 个元素。

⚠️ 这道题的「桶排序」方法也要掌握
> [692.Top K Frequent Words](https://leetcode.com/problems/top-k-frequent-words/)

这道题和`347`很像，但是要注意字典排序

> [451.Sort Characters By Frequency(https://leetcode.com/problems/sort-characters-by-frequency/)

- hashmap to store frequency
- heap to get the most frequent chars ony by one