### 673. Number of Longest Increasing Subsequence

Given an unsorted array of integers, find the number of longest increasing subsequence.

**Example 1:**
```
Input: [1,3,5,4,7]
Output: 2
Explanation: The two longest increasing subsequence are [1, 3, 4, 7] and [1, 3, 5, 7].
```

**Example 2:**
```
Input: [2,2,2,2,2]
Output: 5
Explanation: The length of longest continuous increasing subsequence is 1, and there are 5 subsequences' length is 1, so output 5.
```

**Note:** 
Length of the given array will be not exceed 2000 and the answer is guaranteed to be fit in 32-bit signed int.

**Solution**
```Python
class Solution(object):
    def findNumberOfLIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) <= 1:
            return len(nums)
        
        n = len(nums)
        ans = 1
        max_length = 1
        count = [1] * n
        length = [1] * n

        for i in range(1, n):
            for j in range(i):
                if nums[j] < nums[i]:
                    if length[j] + 1 == length[i]:
                        count[i] += count[j]
                    elif length[j] + 1 > length[i]:
                        count[i] = count[j]
                        length[i] = length[j] + 1
                    
            if max_length == length[i]:
                ans += count[i]
            elif max_length < length[i]:
                max_length = length[i]
                ans = count[i]
        
        return ans
```