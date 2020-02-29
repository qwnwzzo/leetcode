### 160. Intersection of Two Linked Lists

Write a program to find the node at which the intersection of two singly linked lists begins.

**Solution**
```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        if headA is None or headB is None:
            return None
        
        cur_A = headA
        cur_B = headB

        while cur_A != cur_B:
            cur_A = headB if cur_A is None else cur_A.next
            cur_B = headA if cur_B is None else cur_B.next
        
        return cur_A
```