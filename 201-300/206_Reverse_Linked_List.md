### 206. Reverse Linked List

Reverse a singly linked list.

**Example:**
```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

**Follow up:**
```
A linked list can be reversed either iteratively or recursively. Could you implement both?
```

**Solution**
```Python
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
        new_head = None

        while head is not None:
            temp = head.next
            head.next = new_head
            new_head = head
            head = temp
        
        return new_head
```