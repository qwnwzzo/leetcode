### 283. Move Zeroes

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

**Example:**
```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

**Note:**
1. You must do this in-place without making a copy of the array.
2. Minimize the total number of operations.

**Solution**
```Python
class Solution(object):
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        left = 0
        for i in range(len(nums)):
            if nums[i] != 0:
                nums[left], nums[i] = nums[i], nums[left]
                left += 1
```