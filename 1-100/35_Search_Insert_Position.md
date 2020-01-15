### 35. Search Insert Position

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

**Example 1:**
```
Input: [1,3,5,6], 5
Output: 2
```

**Example 2:**
```
Input: [1,3,5,6], 2
Output: 1
```

**Example 3:**
```
Input: [1,3,5,6], 7
Output: 4
```

**Example 4:**
```
Input: [1,3,5,6], 0
Output: 0
```

**Solution**
```Python
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        if len(nums) == 0:
            return 0

        start = 0
        end = len(nums) - 1

        while start + 1 < end:
            mid = start + (end - start) / 2
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                start = mid
            else:
                end = mid
        
        if target <= nums[start]:
            return start
        elif nums[start] < target and target <= nums[end]:
            return end
        else:
            return end + 1
```