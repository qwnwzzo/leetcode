### 674. Longest Continuous Increasing Subsequence

Given an unsorted array of integers, find the length of longest continuous increasing subsequence (subarray).

**Example 1:**
```
Input: [1,3,5,4,7]
Output: 3
Explanation: The longest continuous increasing subsequence is [1,3,5], its length is 3. 
Even though [1,3,5,7] is also an increasing subsequence, it's not a continuous one where 5 and 7 are separated by 4. 
```

**Example 2:**
```
Input: [2,2,2,2,2]
Output: 1
Explanation: The longest continuous increasing subsequence is [2], its length is 1.
```

**Note:** Length of the array will not exceed 10,000.

**Solution**
```Python
class Solution(object):
    def findLengthOfLCIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) <= 1:
            return len(nums)
        
        n = len(nums)
        ans = 1
        left = 0
        right = 1

        while right < len(nums):
            if nums[right] > nums[right - 1]:
                right += 1
            else:
                ans = max(ans, right - left)
                left = right
                right += 1
        
        ans = max(ans, right - left)
        
        return ans
```