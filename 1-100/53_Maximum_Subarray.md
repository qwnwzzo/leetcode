### 53. Maximum Subarray

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

**Example:**
```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

**Follow up:**
```
If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.
```

**Solution**
```Python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        if n == 0:
            return 0
        
        dp = [0] * n
        dp[0] = nums[0]
        ans = nums[0]
        
        for i in range(1, n):
            dp[i] = max(dp[i - 1] + nums[i], nums[i])
            
            if dp[i] > ans:
                ans = dp[i]
                
        return ans
```