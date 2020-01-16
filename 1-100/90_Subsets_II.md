### 90. Subsets II

Given a collection of integers that might contain duplicates, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

**Example:**
```
Input: [1,2,2]
Output:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
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
            if i > start_index and nums[i - 1] == nums[i]:
                continue
            
            subset.append(nums[i])
            self.helper(nums, ans, subset, i + 1)
            subset.pop()

    def subsetsWithDup(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums) == 0:
            return []

        nums.sort()
        ans = []
        subset = []

        self.helper(nums, ans, subset, 0)

        return ans
```