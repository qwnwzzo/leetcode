### 55. Jump Game

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

**Example 1:**
```
Input: [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

**Example 2:**
```
Input: [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.
```

**Solution 1 (TLE)**
```Python
class Solution(object):
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        n = len(nums)
        dp = [False] * n
        dp[0] = True
        
        for i in range(1, n):
            for j in range(i):
                if dp[j] and j + nums[j] >= i:
                    dp[i] = True
                    break
        
        return dp[-1]
```

**Solution 2**
```Python
class Solution(object):
    # record the farthest distance you can jump
    # if you can jump to the last position, return true
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        farthest_index = 0
        for i in range(len(nums)):
            if i > farthest_index:
                return False
            
            farthest_index = max(farthest_index, i + nums[i])
        
        return True
```