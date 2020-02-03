### 203. Remove Linked List Elements

Remove all elements from a linked list of integers that have value val.

**Example:**
```
Input:  1->2->6->3->4->5->6, val = 6
Output: 1->2->3->4->5
```

**Solution**
```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def removeElements(self, head, val):
        """
        :type head: ListNode
        :type val: int
        :rtype: ListNode
        """
        if head is None:
            return None

        dummy_head = ListNode(0)
        dummy_head.next = head
        head = dummy_head

        while head.next is not None:
            if head.next.val == val:
                head.next = head.next.next
            else:
                head = head.next
        
        return dummy_head.next
```