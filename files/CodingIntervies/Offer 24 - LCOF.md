## Question
Define a function that can output the reversed list of the origin ListNode.

## Example
```bash
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

## Solution

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        preNode = None
        currNode = head
        while currNode:
            nextNode = currNode.next
            currNode.next = preNode
            preNode = currNode
            currNode=nextNode

        return preNode
```