### 82. Remove Duplicates from Sorted List II

Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

**Example 1:**
```
Input: 1->2->3->3->4->4->5
Output: 1->2->5
```

**Example 2:**
```
Input: 1->1->1->2->3
Output: 2->3
```

**Solution**
```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        dummy_head = ListNode(0)
        dummy_head.next = head
        head = dummy_head

        while head.next is not None and head.next.next is not None:
            if head.next.val == head.next.next.val:
                val = head.next.val
                while head.next is not None and head.next.val == val:
                    head.next = head.next.next
            else:
                head = head.next

        return dummy_head.next
```