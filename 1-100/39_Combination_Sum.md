### 39. Combination Sum

Given a set of candidate numbers (candidates) (without duplicates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

The same repeated number may be chosen from candidates unlimited number of times.

**Note:**
```
All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.
```

**Example 1:**
```
Input: candidates = [2,3,6,7], target = 7,
A solution set is:
[
  [7],
  [2,2,3]
]
```

**Example 2:**
```
Input: candidates = [2,3,5], target = 8,
A solution set is:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

**Solution**
```Python
class Solution(object):
    def helper(self, candidates, ans, subset, start_index, target):
        subset_sum = sum(subset)
        if subset_sum == target:
            ans.append(subset[:])
            return
        
        if subset_sum > target:
            return

        for i in range(start_index, len(candidates)):
            subset.append(candidates[i])
            self.helper(candidates, ans, subset, i, target)
            subset.pop()

    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        if len(candidates) == 0:
            return []

        ans = []
        subset = []

        self.helper(candidates, ans, subset, 0, target)

        return ans
```