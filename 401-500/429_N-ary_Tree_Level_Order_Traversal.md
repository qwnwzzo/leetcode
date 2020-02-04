### 429. N-ary Tree Level Order Traversal

Given an n-ary tree, return the level order traversal of its nodes' values.

Nary-Tree input serialization is represented in their level order traversal, each group of children is separated by the null value (See examples).

**Constraints:**
- The height of the n-ary tree is less than or equal to 1000
- The total number of nodes is between [0, 10^4]

**Solution**
```Python
"""
# Definition for a Node.
class Node(object):
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""

from Queue import Queue

class Solution(object):
    def levelOrder(self, root):
        """
        :type root: Node
        :rtype: List[List[int]]
        """
        if root is None:
            return []

        q = Queue()
        q.put(root)
        ans = []

        while q.qsize() > 0:
            size = q.qsize()
            level = []

            for i in range(size):
                node = q.get()
                level.append(node.val)
                for child in node.children:
                    q.put(child)

            ans.append(level)
        
        return ans
```