### 23. Merge k Sorted Lists

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

**Example:**
```
Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
```

**Solution**
```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

from Queue import PriorityQueue

class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        
        q = PriorityQueue()
        for l in lists:
            if l is not None:
                q.put([l.val, l])
        
        dummy_head = ListNode(0)
        cur = dummy_head
        
        while q.qsize() > 0:
            val, node = q.get()
            cur.next = node
            cur = cur.next
            if node.next is not None:
                q.put([node.next.val, node.next])
        
        return dummy_head.next
```