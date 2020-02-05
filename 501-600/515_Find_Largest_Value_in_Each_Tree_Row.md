### 515. Find Largest Value in Each Tree Row

You need to find the largest value in each row of a binary tree.

**Example:**
```
Input: 

          1
         / \
        3   2
       / \   \  
      5   3   9 

Output: [1, 3, 9]
```

**Solution**
```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

from Queue import Queue

class Solution(object):
    def largestValues(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if root is None:
            return []

        q = Queue()
        q.put(root)
        
        ans = []

        while q.qsize() > 0:
            size = q.qsize()
            level = []

            for _ in range(size):
                node = q.get()
                level.append(node.val)

                if node.left is not None:
                    q.put(node.left)
                
                if node.right is not None:
                    q.put(node.right)
            
            ans.append(max(level))
        
        return ans
```