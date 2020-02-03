### 300. Longest Increasing Subsequence

Given an unsorted array of integers, find the length of longest increasing subsequence.

**Example:**
```
Input: [10,9,2,5,3,7,101,18]
Output: 4 
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
```

**Note:**
- There may be more than one LIS combination, it is only necessary for you to return the length.
- Your algorithm should run in O(n2) complexity.
Follow up: Could you improve it to O(n log n) time complexity?

**Solution**
```Python
class Solution(object):
    def lengthOfLIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) == 0:
            return 0

        ans = 1
        dp = [1] * len(nums)

        for i in range(1, len(nums)):
            max_val = 0
            for j in range(i):
                if nums[j] < nums[i]:
                    max_val = max(max_val, dp[j])
            
            dp[i] = max_val + 1
            ans = max(ans, dp[i])
        
        return ans
```