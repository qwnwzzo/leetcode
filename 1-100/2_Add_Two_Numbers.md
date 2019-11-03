### 2. Add Two Numbers

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**
```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

**Solution**
```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        dummy_head = ListNode(0)
        cur = dummy_head
        carry = 0
        
        while l1 is not None and l2 is not None:
            s = l1.val + l2.val + carry
            carry = s / 10
            s = s % 10
            node = ListNode(s)
            cur.next = node
            cur = cur.next
            
            l1 = l1.next
            l2 = l2.next
            
        if l1 is not None:
            while l1 is not None:
                s = l1.val + carry
                carry = s / 10
                s = s % 10
                node = ListNode(s)
                cur.next = node
                cur = cur.next
                
                l1 = l1.next
        elif l2 is not None:
            while l2 is not None:
                s = l2.val + carry
                carry = s / 10
                s = s % 10
                node = ListNode(s)
                cur.next = node
                cur = cur.next
                
                l2 = l2.next
        
        if carry > 0:
            node = ListNode(carry)
            cur.next = node
        
        return dummy_head.next
```