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
 我觉得最开始接触到这道题的难点时不知道怎么用「最小堆」。本题使用了python `heapq`模块
- `heapq.heapify`, 原地把 list 调成堆，其中第一个元素是最小的元素
- `heapq.heappop`,  弹出堆顶元素
- `heapq.heappush`, 将新元素增加到堆中
- `heapq.heapreplace`, 替换堆顶元素
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

> [451.Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency/)

- hashmap to store frequency
- heap to get the most frequent chars ony by one

> [857. Minimum Cost to Hire K Workers](https://leetcode.com/problems/minimum-cost-to-hire-k-workers/)

`hard`

### 第 K 大元素
> [703. Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/)

求数据流中第 K 大元素。一个大小为 K 的最小堆存较大的 K 个数，小于堆顶元素则放弃，大于堆顶元素则入堆，堆顶即为第 K 大元素。
> [215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

Similar to `703`, pay attention to `quick sort` method

> [378. Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)

在二维矩阵中找第K小的数。同样是找第K小的数，只是变为了二维数组，用一个大小为K存较小元素的大顶堆，小于堆顶的元素可以入堆，遍历完后堆顶即为结果。Be careflul the way to construct heap

> [264. Ugly Number II](https://leetcode.com/problems/ugly-number-ii/)

求返回第 n 个丑数。暴力破解求前 n 个丑数，放到大小为 n 的堆中，堆顶即为第 n 个丑数。

> [313. Super Ugly Number](https://leetcode.com/problems/super-ugly-number/)

跟上面这道题几乎一样，只是质因子的定义不同了

### 找中位数
> [295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)

求数据流中的中位数。其实中位数问题只是特殊的`第k大元素的问题`。构造一个最小堆（存大于等于中位数的所有数）和一个最大堆（存小于等于中位数的所有数），保持最小堆的元素数量最多比最大堆的元素数量多1. 那么最后中位数就是两堆堆顶的平均值或者，最小堆的堆顶。

### 堆排序
> [1046. Last Stone Weight](https://leetcode.com/problems/last-stone-weight/)

`medium`. 每次选最大的两块石头粉碎，为了实现每次都取到最大的石头，我们用`heap`数据结构

> [355.Design Twitter](https://leetcode.com/problems/design-twitter/)

`hard`。 用`heap`结构来表示最近访问的 tweets.