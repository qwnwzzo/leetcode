### 209. Minimum Size Subarray Sum

Given an array of **n** positive integers and a positive integer **s**, find the minimal length of a **contiguous** subarray of which the sum ≥ **s**. If there isn't one, return 0 instead.

**Example:** 
```
Input: s = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: the subarray [4,3] has the minimal length under the problem constraint.
```

**Follow up:**
If you have figured out the O(n) solution, try coding another solution of which the time complexity is O(n log n). 

**Solution**
```Python
class Solution(object):
    def minSubArrayLen(self, s, nums):
        """
        :type s: int
        :type nums: List[int]
        :rtype: int
        """
        left = 0
        sum_num = 0
        ans = float("inf")

        for i in range(len(nums)):
            sum_num += nums[i]
            while sum_num >= s:
                ans = min(ans, i - left + 1)
                sum_num -= nums[left]
                left += 1
        
        return ans if ans != float("inf") else 0
```