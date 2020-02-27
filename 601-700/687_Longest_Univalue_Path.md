### 687. Longest Univalue Path

Given a binary tree, find the length of the longest path where each node in the path has the same value. This path may or may not pass through the root.

The length of path between two nodes is represented by the number of edges between them.

**Example 1:**
```
Input:

              5
             / \
            4   5
           / \   \
          1   1   5
Output: 2
```

**Example 2:**
```
Input:

              1
             / \
            4   5
           / \   \
          4   4   5
Output: 2
```
 
**Note:** The given binary tree has not more than 10000 nodes. The height of the tree is not more than 1000.

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
    
    def helper(self, node):
        if node is None:
            return 0
        
        if node.left is None and node.right is None:
            return 0
        
        left_num_e = self.helper(node.left)
        right_num_e = self.helper(node.right)

        if node.left is not None and node.val == node.left.val:
            left_num_e += 1
        else:
            left_num_e = 0
        
        if node.right is not None and node.val == node.right.val:
            right_num_e += 1
        else:
            right_num_e = 0
        
        self.ans = max(self.ans, left_num_e + right_num_e)

        return max(left_num_e, right_num_e)

    def longestUnivaluePath(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if root is None:
            return 0
        
        self.helper(root)

        return self.ans
```