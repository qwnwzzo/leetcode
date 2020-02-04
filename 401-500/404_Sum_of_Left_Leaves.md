### 404. Sum of Left Leaves

Find the sum of all left leaves in a given binary tree.

**Example:**
```
    3
   / \
  9  20
    /  \
   15   7

There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
```

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
        self.ans = 0

    def helper(self, node, is_left):
        if node is None:
            return
        
        if is_left and node.left is None and node.right is None:
            self.ans += node.val
            return
        
        self.helper(node.left, True)
        self.helper(node.right, False)

    def sumOfLeftLeaves(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        self.helper(root, False)

        return self.ans
```