### 78. Subsets

Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

**Example:**
```
Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

**Solution**
```Python
class Solution(object):
    def helper(self, nums, ans, subset, start_index):
        if start_index == len(nums):
            ans.append(subset[:])
            return

        ans.append(subset[:])
        for i in range(start_index, len(nums)):
            subset.append(nums[i])
            self.helper(nums, ans, subset, i + 1)
            subset.pop()

    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums) == 0:
            return []

        ans = []
        subset = []

        self.helper(nums, ans, subset, 0)

        return ans
```