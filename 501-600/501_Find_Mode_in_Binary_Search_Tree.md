### 501. Find Mode in Binary Search Tree

Given a binary search tree (BST) with duplicates, find all the mode(s) (the most frequently occurred element) in the given BST.

Assume a BST is defined as follows:
- The left subtree of a node contains only nodes with keys less than or equal to the node's key.
- The right subtree of a node contains only nodes with keys greater than or equal to the node's key.
- Both the left and right subtrees must also be binary search trees.
 

**For example:**
```
Given BST [1,null,2,2],

   1
    \
     2
    /
   2
 

return [2].
```

**Note:** If a tree has more than one mode, you can return them in any order.

**Follow up:** Could you do that without using any extra space? (Assume that the implicit stack space incurred due to recursion does not count).

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
        self.freq_m = {}
        self.max_freq = -float("inf")

    def helper(self, node):
        if node is None:
            return
        
        self.helper(node.left)

        if node.val not in self.freq_m:
            self.freq_m[node.val] = 0
        self.freq_m[node.val] += 1
        self.max_freq = max(self.max_freq, self.freq_m[node.val])

        self.helper(node.right)

    def findMode(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if root is None:
            return []
        
        self.helper(root)
        ans = []
        for val in self.freq_m:
            if self.freq_m[val] == self.max_freq:
                ans.append(val)
        
        return ans
```