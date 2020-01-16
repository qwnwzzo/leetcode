### 46. Permutations

Given a collection of distinct integers, return all possible permutations.

**Example:**
```
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

**Solution**
```Python
class Solution(object):
    def helper(self, nums, ans, subset, visited):
        if len(subset) == len(nums):
            ans.append(subset[:])
            return

        for i in range(len(nums)):
            if not visited[i]:
                subset.append(nums[i])
                visited[i] = True
                self.helper(nums, ans, subset, visited)
                visited[i] = False
                subset.pop()

    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums) == 0:
            return []

        ans = []
        subset = []
        visited = [False] * len(nums)
        self.helper(nums, ans, subset, visited)

        return ans
```