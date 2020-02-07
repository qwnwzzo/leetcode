### 41. First Missing Positive

Given an unsorted integer array, find the smallest missing positive integer.

**Example 1:**
```
Input: [1,2,0]
Output: 3
```

**Example 2:**
```
Input: [3,4,-1,1]
Output: 2
```

**Example 3:**
```
Input: [7,8,9,11,12]
Output: 1
```

**Note:**
Your algorithm should run in O(n) time and uses constant extra space.

**Solution**
```Python
class Solution(object):
    def firstMissingPositive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)

        for i in range(n):
            while nums[i] >= 1 and nums[i] <= n and i != nums[i] - 1 and nums[i] != nums[nums[i] - 1]:
                temp = nums[i] - 1
                nums[i], nums[temp] = nums[temp], nums[i]
        
        for i in range(n):
            if i + 1 != nums[i]:
                return i + 1
        
        return n + 1
```