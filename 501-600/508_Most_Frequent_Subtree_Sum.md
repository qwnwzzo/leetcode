### 508. Most Frequent Subtree Sum

Given the root of a tree, you are asked to find the most frequent subtree sum. The subtree sum of a node is defined as the sum of all the node values formed by the subtree rooted at that node (including the node itself). So what is the most frequent subtree sum value? If there is a tie, return all the values with the highest frequency in any order.

**Examples 1**
Input:
```

  5
 /  \
2   -3
```
return [2, -3, 4], since all the values happen only once, return all of them in any order.

**Examples 2**
Input:
```

  5
 /  \
2   -5
```
return [2], since 2 happens twice, however -5 only occur once.

**Note:** You may assume the sum of values in any subtree is in the range of 32-bit signed integer.

**Solution**
```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def helper(self, node, freq_m):
        if node is None:
            return 0

        left = self.helper(node.left, freq_m)
        right = self.helper(node.right, freq_m)

        sum_val = node.val + left + right
        if sum_val not in freq_m:
            freq_m[sum_val] = 0
        freq_m[sum_val] += 1

        return sum_val

    def findFrequentTreeSum(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if root is None:
            return []

        freq_m = {}
        self.helper(root, freq_m)

        max_freq = 0
        for val in freq_m:
            max_freq = max(max_freq, freq_m[val])
        
        ans = []
        for val in freq_m:
            if freq_m[val] == max_freq:
                ans.append(val)
        
        return ans
```