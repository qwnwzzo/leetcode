### 513. Find Bottom Left Tree Value

Given a binary tree, find the leftmost value in the last row of the tree.

**Example 1:**
```
Input:

    2
   / \
  1   3

Output:
1
```

**Example 2:**
```
Input:

        1
       / \
      2   3
     /   / \
    4   5   6
       /
      7

Output:
7
```

**Note:** You may assume the tree (i.e., the given root node) is not NULL.

**Solution**
```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def __init__(self):
        self.max_depth = -1
        self.ans = 0
    
    def helper(self, node, depth):
        if node is None:
            return
        
        if node.left is None and node.right is None:
            if depth > self.max_depth:
                self.max_depth = depth
                self.ans = node.val
            return
        
        self.helper(node.left, depth + 1)
        self.helper(node.right, depth + 1)

    def findBottomLeftValue(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        self.helper(root, 0)
        return self.ans
```