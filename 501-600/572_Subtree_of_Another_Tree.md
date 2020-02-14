### 572. Subtree of Another Tree

Given two non-empty binary trees **s** and **t**, check whether tree **t** has exactly the same structure and node values with a subtree of **s**. A subtree of s is a tree consists of a node in **s** and all of this node's descendants. The tree **s** could also be considered as a subtree of itself.

**Example 1:**
```
Given tree s:

     3
    / \
   4   5
  / \
 1   2
Given tree t:
   4 
  / \
 1   2
Return true, because t has the same structure and node values with a subtree of s.
```

**Example 2:**
```
Given tree s:

     3
    / \
   4   5
  / \
 1   2
    /
   0
Given tree t:
   4
  / \
 1   2
Return false.
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
    def helper(self, node, t):
        if node is None and t is None:
            return True
        elif node is None:
            return False
        elif t is None:
            return False
        elif node.val != t.val:
            return False
        
        return self.helper(node.left, t.left) and self.helper(node.right, t.right)

    def isSubtree(self, s, t):
        """
        :type s: TreeNode
        :type t: TreeNode
        :rtype: bool
        """
        if s is None and t is None:
            return True
        elif s is None:
            return False
        elif t is None:
            return False
        elif self.helper(s, t):
            return True
        
        return self.isSubtree(s.left, t) or self.isSubtree(s.right, t)
```