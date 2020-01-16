### 47. Permutations II

Given a collection of numbers that might contain duplicates, return all possible unique permutations.

**Example:**
```
Input: [1,1,2]
Output:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
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
            if visited[i]:
                continue

            if i > 0 and nums[i - 1] == nums[i] and not visited[i - 1]:
                continue
            
            subset.append(nums[i])
            visited[i] = True
            self.helper(nums, ans, subset, visited)
            visited[i] = False
            subset.pop()

    def permuteUnique(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums) == 0:
            return []

        nums.sort()

        ans = []
        subset = []
        visited = [False] * len(nums)

        self.helper(nums, ans, subset, visited)

        return ans
```