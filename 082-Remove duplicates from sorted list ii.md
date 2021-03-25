## Problem
Given the head of a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list sorted as well.

## Example
![](https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg)
```bash
Input: head = [1,2,3,3,4,4,5]
Output: [1,2,5]
```

![](https://assets.leetcode.com/uploads/2021/01/04/linkedlist2.jpg)
```bash
Input: head = [1,1,1,2,3]
Output: [2,3]
```
## Solution
```python
class Solution(object):
    def deleteDuplicates(self, head):
        if not head or not head.next:
            return head
        if head.val != head.next.val:
            head.next = self.deleteDuplicates(head.next)
        else:
            move = head.next
            # This while loop is important when you meet more than three consecutive identical integers
            while move and head.val == move.val:
                move = move.next
            return self.deleteDuplicates(move)
        return head
```
Runtime: 24 ms