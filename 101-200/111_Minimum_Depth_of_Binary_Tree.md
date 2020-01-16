### 111. Minimum Depth of Binary Tree

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

Note: A leaf is a node with no children.

**Example:**
```
Given binary tree [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
```
return its minimum depth = 2.

**Solution**
```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def helper(self, node):
        if node is None:
            return 0
        
        left_depth = self.helper(node.left)
        right_depth = self.helper(node.right)

        if left_depth > 0 and right_depth == 0:
            return left_depth + 1
        elif left_depth == 0 and right_depth > 0:
            return right_depth + 1
        
        return min(left_depth, right_depth) + 1

    def minDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if root is None:
            return 0

        return self.helper(root)
```