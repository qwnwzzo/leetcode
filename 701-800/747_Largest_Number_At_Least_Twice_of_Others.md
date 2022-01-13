### 747. Largest Number At Least Twice of Others

In a given integer array `nums`, there is always exactly one largest element.

Find whether the largest element in the array is at least twice as much as every other number in the array.

If it is, return the **index** of the largest element, otherwise return -1.

**Example 1:**
```
Input: nums = [3, 6, 1, 0]
Output: 1
Explanation: 6 is the largest integer, and for every other number in the array x,
6 is more than twice as big as x.  The index of value 6 is 1, so we return 1.
```

**Example 2:**
```
Input: nums = [1, 2, 3, 4]
Output: -1
Explanation: 4 isn't at least as big as twice the value of 3, so we return -1.
```

**Note:**
- nums will have a length in the range [1, 50].
- Every nums[i] will be an integer in the range [0, 99].

**Solution 01**
```python
class Solution(object):
    def dominantIndex(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) == 0:
            return -1

        max_num = nums[0]
        max_index = 0
        for i in range(1, len(nums)):
            if max_num < nums[i]:
                max_num = nums[i]
                max_index = i
        
        for i in range(len(nums)):
            if i != max_index:
                if nums[i] * 2 > max_num:
                    return -1
        
        return max_index
```

**Solution 02**
```python
class Solution(object):
    def dominantIndex(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        if n == 1:
            return 0
        
        largest = -1
        sec_largest = -1
        index = -1
        for i in range(n):
            if nums[i] > sec_largest and nums[i] < largest:
                sec_largest = nums[i]
            elif nums[i] > largest:
                sec_largest = largest
                largest = nums[i]
                index = i
        
        return index if largest >= sec_largest * 2 else -1
```