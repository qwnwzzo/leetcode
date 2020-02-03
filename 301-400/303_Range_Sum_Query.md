### 303. Range Sum Query - Immutable

Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

**Example:**
```
Given nums = [-2, 0, 3, -5, 2, -1]

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
```

**Note:**
- You may assume that the array does not change.
- There are many calls to sumRange function.

**Solution**
```Python
class NumArray(object):

    def __init__(self, nums):
        """
        :type nums: List[int]
        """
        self.nums = nums
        if len(nums) == 0:
            self.sum_nums = []
        else:
            self.sum_nums = [0] * len(nums)
            self.sum_nums[0] = nums[0]
            for i in range(1, len(nums)):
                self.sum_nums[i] = nums[i] + self.sum_nums[i - 1]

    def sumRange(self, i, j):
        """
        :type i: int
        :type j: int
        :rtype: int
        """
        return self.nums[i] + self.sum_nums[j] - self.sum_nums[i]


# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# param_1 = obj.sumRange(i,j)
```