### 450. Delete Node in a BST

Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.

Basically, the deletion can be divided into two stages:

Search for a node to remove.
If the node is found, delete the node.
Note: Time complexity should be O(height of tree).

**Example:**
```
root = [5,3,6,2,4,null,7]
key = 3

    5
   / \
  3   6
 / \   \
2   4   7

Given key to delete is 3. So we find the node with value 3 and delete it.

One valid answer is [5,4,6,2,null,null,7], shown in the following BST.

    5
   / \
  4   6
 /     \
2       7

Another valid answer is [5,2,6,null,4,null,7].

    5
   / \
  2   6
   \   \
    4   7
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
    def get_min_node(self, node):
        if node.left is None:
            return node
        
        return self.get_min_node(node.left)

    def delete_min_node(self, node):
        if node.left is None:
            return node.right
        
        node.left = self.delete_min_node(node.left)

        return node

    def deleteNode(self, root, key):
        """
        :type root: TreeNode
        :type key: int
        :rtype: TreeNode
        """
        if root is None:
            return None
        
        if root.val < key:
            root.right = self.deleteNode(root.right, key)
            return root
        
        if root.val > key:
            root.left = self.deleteNode(root.left, key)
            return root
        
        if root.left is None:
            return root.right

        if root.right is None:
            return root.left
        
        min_node = self.get_min_node(root.right)
        copy_min_node = TreeNode(min_node.val)
        copy_min_node.left = root.left
        copy_min_node.right = self.delete_min_node(root.right)

        return copy_min_node
```