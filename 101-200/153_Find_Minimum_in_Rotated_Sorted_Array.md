### 153. Find Minimum in Rotated Sorted Array

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e.,  `[0,1,2,4,5,6,7]` might become  `[4,5,6,7,0,1,2]`).

Find the minimum element.

You may assume no duplicate exists in the array.

**Example 1:**
```
Input: [3,4,5,1,2] 
Output: 1
```

**Example 2:**
```
Input: [4,5,6,7,0,1,2]
Output: 0
```

**Idea**
```
使用target记录数组最右端的数字，然后用start和end标志寻找区间，如果mid位置上的数字小于等于最右端的数字时，区间向左移动，其余向右移动即可，返回start和end位置上较小值即可。
```

**Solution**
```Python
class Solution(object):
    def findMin(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        start = 0
        end = len(nums) - 1
        target = nums[-1]

        while start + 1 < end:
            mid = start + (end - start) / 2
            if nums[mid] <= target:
                end = mid
            else:
                start = mid
        
        if nums[start] < nums[end]:
            return nums[start]

        return nums[end]
```