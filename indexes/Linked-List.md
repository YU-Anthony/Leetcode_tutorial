> 参考资料：
> 1. [代码随想录-链表总结篇](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/%E9%93%BE%E8%A1%A8%E6%80%BB%E7%BB%93%E7%AF%87.md)
> 2. [力扣刷题总结之链表](https://leetcode.cn/circle/article/YGr54o/)

# 1. 理论基础
- 链表的种类：单向链表，双向链表，循环链表
- 链表的存储方式：链表的节点在内存中分散存储，通过指针连在一起
- 链表的基础操作：增删改查

# 2. 常见题目
## 2.1 链表的基础操作
### 设计链表
> [707. Design Linked List](https://leetcode.com/problems/design-linked-list/)

这是一道非常经典的题目，可以联系链表的基础操作 -「增删改查」
- 获取链表第 index 节点的值
- 在链表头部插入节点
- 在链表尾部插入节点
- 在任意位置插入节点
- 删除任意位置节点
### 删除重复元素
>[82. Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/)<br>
>[83. Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/)

「`迭代法`」和「`递归法`」都需要掌握

### 反转链表
> [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)<br>
> [25. Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/)

反转链表考的频次非常高，我觉得`迭代法`和`递归法`都需要掌握

### 链表相交
> [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)

思路就是先移动头节点使得两条链表剩余的长度一样，然后同时移动两条链表的头指针，如果存在链表相交的情况，那两个头节点一定会同时走到相同的位置。

### 合并多条链表
> [21. Merged Two Sorted List](https://leetcode.com/problems/merge-two-sorted-lists/) <br>
> [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)

`21题` 就是常规的用`迭代`和`递归`去解决，`23题` 虽然是`hard`,但其实这道题的思路很简单，就是俩俩先合并，直到合并到最后只剩一个 list。

### 链表分解
> [86. Partition List](https://leetcode.com/problems/partition-list/)

前面我们做过了合并链表，今天这道题的思想则是`分解链表`。具体来说就是将原链表分成两个小链表，一个链表的元素都小于x,另一个链表的元素都大于等于x,最后将两个链表合并起来。但要注意`虚拟头节点`的运用。

### 寻找链表中点 + 反转链表 + 合并链表
> [143.Reorder List](https://leetcode.cn/problems/reorder-list/)

超级经典的一道题，必刷！！！链表的很多考法都涉及到了

## 2.2 进阶题目
### 双向链表
> [146. LRU Cache](https://leetcode.cn/problems/lru-cache/)

双向链表可以双向查询，本题运用了 `「哈希表」`+`「双向链表」`的思想，是一道经典的设计题，

### 环形链表
> [141. Linked Cycle List](https://leetcode.com/problems/linked-list-cycle/)

`快慢指针`。若存在环，快慢指针迟早会相遇；若不存在环，快指针一定会先走到链表尾部。

> [142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)

`快慢指针`。首先用`141`的方法判断是否有环，然后让相遇后的`fast`指向头节点，再让fast和slow同时走，相遇的地方就是环的入口。
### 链表 + 双指针
>[876.Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)

经典的「`快慢指针`」的问题，每次快指针比慢指针多走一步。

> [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

这道题用到了「`快慢指针`」，让`fast`先走n步，然后同时移动`fast`和`slow`，等`fast `走到终点了，删除`slow`指针对应的节点即可。
> [234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)

「`快慢指针`」。快指针走两步，慢指针走一步，找到链表中点，然后反转后半部分链表，看看两个链表是否一样。

### 链表排序
> [147. Insertion Sort List](https://leetcode.com/problems/insertion-sort-list/)

`插入排序`。首先找到需要重新排序的节点，然后重新从链表头部开始寻找插入点。

## 2.3 其他经典题目
- [138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/)  `模拟题`。模拟链表的拷贝。需要用到「`哈希表`」的知识。
- [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/) `模拟题`。从左至右遍历两个链表模拟加法运算。


