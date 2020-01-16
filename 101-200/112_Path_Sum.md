### 112. Path Sum

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

Note: A leaf is a node with no children.

**Example:**

Given the below binary tree and sum = 22,
```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
```
return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.

**Solution**
```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def helper(self, target, node, cur_sum):
        if node is None:
            return False
        
        if node.left is None and node.right is None:
            return cur_sum + node.val == target
        
        left_check = self.helper(target, node.left, cur_sum + node.val)
        right_check = self.helper(target, node.right, cur_sum + node.val)

        return left_check or right_check

    def hasPathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: bool
        """
        if root is None:
            return False

        return self.helper(sum, root, 0)
```