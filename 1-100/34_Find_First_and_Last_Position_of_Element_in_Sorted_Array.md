### 34. Find First and Last Position of Element in Sorted Array

Given an array of integers nums sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

**Example 1:**
```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

**Example 2:**
```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

**Solution**
```Python
class Solution(object):
    def find_first_position(self, nums, target):
        start = 0
        end = len(nums) - 1

        while start + 1 < end:
            mid = start + (end - start) / 2
            if nums[mid] == target:
                end = mid
            elif nums[mid] > target:
                end = mid
            else:
                start = mid
        
        if nums[start] == target:
            return start
        
        if nums[end] == target:
            return end

        return -1
    
    def find_last_position(self, nums, target):
        start = 0
        end = len(nums) - 1

        while start + 1 < end:
            mid = start + (end - start) / 2
            if nums[mid] == target:
                start = mid
            elif nums[mid] > target:
                end = mid
            else:
                start = mid
        
        if nums[end] == target:
            return end
        
        if nums[start] == target:
            return start

        return -1

    def searchRange(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        if len(nums) == 0:
            return [-1, -1]

        first_position = self.find_first_position(nums, target)
        if first_position == -1:
            return [-1, -1]

        last_position = self.find_last_position(nums, target)

        return [first_position, last_position]
```