### 24. Swap Nodes in Pairs

Given a linked list, swap every two adjacent nodes and return its head.

You may not modify the values in the list's nodes, only nodes itself may be changed.

**Example:**
```
Given 1->2->3->4, you should return the list as 2->1->4->3.
```

**Solution**
```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def swapPairs(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        dummy_head = ListNode(0)
        dummy_head.next = head
        pre = dummy_head

        while head is not None and head.next is not None:
            a = head
            b = head.next
            temp = b.next

            pre.next = b
            pre = pre.next
            pre.next = a
            pre = pre.next

            head = temp
        
        pre.next = head

        return dummy_head.next
```