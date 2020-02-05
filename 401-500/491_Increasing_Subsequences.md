### 491. Increasing Subsequences

Given an integer array, your task is to find all the different possible increasing subsequences of the given array, and the length of an increasing subsequence should be at least 2.

**Example:**
```
Input: [4, 6, 7, 7]
Output: [[4, 6], [4, 7], [4, 6, 7], [4, 6, 7, 7], [6, 7], [6, 7, 7], [7,7], [4,7,7]]
```

**Note:**
- The length of the given array will not exceed 15.
- The range of integer in the given array is [-100,100].
- The given array may contain duplicates, and two equal integers should also be considered as a special case of increasing sequence.

**Solution**
```Python
class Solution(object):
    def helper(self, nums, ans, subset, start_index):
        if start_index == len(nums):
            if len(subset) >= 2:
                ans.append(subset[:])
            return

        if len(subset) >= 2:
            ans.append(subset[:])

        set_helper = set()
        for i in range(start_index, len(nums)):
            if i > start_index and nums[i] in set_helper:
                continue

            if len(subset) == 0 or nums[i] >= subset[-1]:
                subset.append(nums[i])
                set_helper.add(nums[i])
                self.helper(nums, ans, subset, i + 1)
                subset.pop()

    def findSubsequences(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums) <= 1:
            return []
        
        ans = []
        subset = []
        self.helper(nums, ans, subset, 0)

        return ans
```