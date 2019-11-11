### 1161. Maximum Level Sum of a Binary Tree

Given the root of a binary tree, the level of its root is 1, the level of its children is 2, and so on.

Return the smallest level X such that the sum of all the values of nodes at level X is maximal.

**Note:**

- The number of nodes in the given tree is between 1 and 10^4.
- -10^5 <= node.val <= 10^5

**Solution**
```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def maxLevelSum(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        ans = -1
        max_val = -float("inf")
        queue = [root]
        i = 0

        while len(queue) > 0:
            i += 1
            size = len(queue)
            level = []
            for _ in range(size):
                n = queue.pop(0)
                level.append(n.val)
                if n.left is not None:
                    queue.append(n.left)
                if n.right is not None:
                    queue.append(n.right)
            
            level_sum = sum(level)
            if level_sum > max_val:
                max_val = level_sum
                ans = i
        
        return ans
```