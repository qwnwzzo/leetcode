### 116. Populating Next Right Pointers in Each Node

You are given a **perfect binary tree** where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:
```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to **NULL**.

Initially, all next pointers are set to **NULL**.

**Follow up:**
```
You may only use constant extra space.
Recursive approach is fine, you may assume implicit stack space does not count as extra space for this problem.
```

**Solution**
```Python
"""
# Definition for a Node.
class Node(object):
    def __init__(self, val=0, left=None, right=None, next=None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""
class Solution(object):
    def connect(self, root):
        """
        :type root: Node
        :rtype: Node
        """
        if root is None:
            return root

        left = root.left
        right = root.right

        while left:
            left.next = right
            left = left.right
            right = right.left
        
        self.connect(root.left)
        self.connect(root.right)

        return root
```