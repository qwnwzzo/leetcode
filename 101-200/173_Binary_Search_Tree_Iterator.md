### 173. Binary Search Tree Iterator

Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.

Calling `next()` will return the next smallest number in the BST.

**Note:**
- `next()` and `hasNext()` should run in average O(1) time and uses O(h) memory, where h is the height of the tree.
- You may assume that `next()` call will always be valid, that is, there will be at least a next smallest number in the BST when `next()` is called.

**Solution**
```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class BSTIterator(object):
    def mid_order_traverse(self, node, ans):
        if node is None:
            return
        
        self.mid_order_traverse(node.left, ans)
        ans.append(node)
        self.mid_order_traverse(node.right, ans)

    def __init__(self, root):
        """
        :type root: TreeNode
        """
        self.queue = []
        self.mid_order_traverse(root, self.queue)

    def next(self):
        """
        @return the next smallest number
        :rtype: int
        """
        return self.queue.pop(0).val

    def hasNext(self):
        """
        @return whether we have a next smallest number
        :rtype: bool
        """
        return len(self.queue) > 0


# Your BSTIterator object will be instantiated and called as such:
# obj = BSTIterator(root)
# param_1 = obj.next()
# param_2 = obj.hasNext()
```