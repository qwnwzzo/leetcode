416. Partition Equal Subset Sum (zero one pack)

Given a **non-empty** array containing **only positive integers**, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

**Note:**
1. Each of the array element will not exceed 100.
2. The array size will not exceed 200.
 
**Example 1:**
```
Input: [1, 5, 11, 5]

Output: true

Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

**Example 2:**
```
Input: [1, 2, 3, 5]

Output: false

Explanation: The array cannot be partitioned into equal sum subsets.
```

**Solution**
```Python
class Solution(object):
    def canPartition(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        n = len(nums)
        sum_val = sum(nums)
        if sum_val & 1 == 1:
            return False

        target = sum_val / 2
        dp = [False] * (target + 1)
        dp[0] = True

        for i in range(n):
            for w in range(target, nums[i] - 1, -1):
                dp[w] = dp[w] or dp[w - nums[i]]
        
        return dp[target]
```