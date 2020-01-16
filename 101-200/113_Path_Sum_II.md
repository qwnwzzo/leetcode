### 113. Path Sum II

Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

Note: A leaf is a node with no children.

**Example:**
```
Given the below binary tree and sum = 22,

      5
     / \
    4   8
   /   / \
  11  13  4
 /  \    / \
7    2  5   1
Return:

[
   [5,4,11,2],
   [5,8,4,5]
]
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
    def helper(self, target, node, ans, subset, cur_sum):
        if node is None:
            return
        
        if node.left is None and node.right is None:
            if cur_sum + node.val == target:
                subset.append(node.val)
                ans.append(subset[:])
                subset.pop()
            return
        
        subset.append(node.val)
        self.helper(target, node.left, ans, subset, cur_sum + node.val)
        self.helper(target, node.right, ans, subset, cur_sum + node.val)
        subset.pop()

    def pathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: List[List[int]]
        """
        if root is None:
            return []

        ans = []
        subset = []

        self.helper(sum, root, ans, subset, 0)

        return ans
```