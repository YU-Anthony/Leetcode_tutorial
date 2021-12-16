这道题跟 [二叉搜索树的最近公共祖先类似](https://github.com/YU-Anthony/Leetcode_tutorial/blob/main/Tree/235.%20Lowest%20Common%20Ancestor%20of%20a%20Binary%20Search%20Tree.md) 
只是要比那个难一点。

# Question
给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉树:  root = [3,5,1,6,2,0,8,null,null,7,4]

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/15/binarytree.png)

Example 1:
```bash
输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
输出: 3
解释: 节点 5 和节点 1 的最近公共祖先是节点 3。
```
Example 2:
```bash
输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
输出: 5
解释: 节点 5 和节点 4 的最近公共祖先是节点 5。因为根据定义最近公共祖先节点可以为节点本身。
```
# Answer
我们要考虑这么几种情况
1. 如果 root 是 None, 则返回 root (None)
2. 如果 root 等于 p,q 中任意一个，则返回 root
3. 如果 root 不等于 p,q 中任何一个，则：

  a. 如果左子树没找到，则在右子树中，返回 lowestCommonAncestor(root.right, p , q)
  
  b. 如果右子树没找到，则在左子树中，返回 lowestCommonAncestor(root.left, p , q)
  
  c. 如果左右子树分别找到，则返回 root
  
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
        if not root or root==p or root==q:
            return root

        left = self.lowestCommonAncestor(root.left,p,q)
        right = self.lowestCommonAncestor(root.right,p,q)

        return root if left and right else left or right
```
