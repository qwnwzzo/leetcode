### 863. All Nodes Distance K in Binary Tree

We are given a binary tree (with root node root), a target node, and an integer value K.

Return a list of the values of all nodes that have a distance K from the target node.  The answer can be returned in any order.

**Example 1:**
```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], target = 5, K = 2

Output: [7,4,1]

Explanation: 
The nodes that are a distance 2 from the target node (with value 5)
have values 7, 4, and 1.

Note that the inputs "root" and "target" are actually TreeNodes.
The descriptions of the inputs above are just serializations of these objects.
```

**Note:**
- The given tree is non-empty.
- Each node in the tree has unique values 0 <= node.val <= 500.
- The target node is a node in the tree.
- 0 <= K <= 1000.

**Solution**
```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

from Queue import Queue

class Solution(object):
    def helper(self, m, node, parent):
        if node is None:
            return

        m[node] = []
        if parent is not None:
            m[node].append(parent)
        
        if node.left is not None:
            m[node].append(node.left)
            self.helper(m, node.left, node)
        
        if node.right is not None:
            m[node].append(node.right)
            self.helper(m, node.right, node)

    def distanceK(self, root, target, K):
        """
        :type root: TreeNode
        :type target: TreeNode
        :type K: int
        :rtype: List[int]
        """
        if root is None:
            return []
        
        if K == 0:
            return [target.val]
        
        m = {}
        self.helper(m, root, None)

        visited = set()
        q = Queue()
        q.put(target)
        level = []
        for i in range(K + 1):
            size = q.qsize()
            if size == 0:
                return []
            
            level = []
            for _ in range(size):
                node = q.get()
                level.append(node.val)
                visited.add(node)
                for neighbour in m[node]:
                    if neighbour not in visited:
                        q.put(neighbour)
        
        return level
```