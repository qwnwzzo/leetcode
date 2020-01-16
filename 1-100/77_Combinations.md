### 77. Combinations

Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

**Example:**
```
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

**Solution**
```Python
class Solution(object):
    def helper(self, nums, ans, subset, k, start_index):
        if len(subset) == k:
            ans.append(subset[:])
            return
        
        for i in range(start_index, len(nums)):
            subset.append(nums[i])
            self.helper(nums, ans, subset, k, i + 1)
            subset.pop()

    def combine(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: List[List[int]]
        """
        if n == 0 or k > n:
            return []

        ans = []
        subset = []
        nums = [i+ 1 for i in range(n)]

        self.helper(nums, ans, subset, k, 0)

        return ans
```