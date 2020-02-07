### 442. Find All Duplicates in an Array

Given an array of integers, 1 ≤ a[i] ≤ n (n = size of array), some elements appear **twice** and others appear **once**.

Find all the elements that appear **twice** in this array.

Could you do it without extra space and in O(n) runtime?

**Example:**
```
Input:
[4,3,2,7,8,2,3,1]

Output:
[2,3]
```

**Solution**
```
class Solution(object):
    def findDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        if len(nums) == 0:
            return []

        n = len(nums)
        ans = []
        for i in range(n):
            while i != nums[i] - 1 and nums[i] != nums[nums[i] - 1]:
                temp = nums[i] - 1
                nums[i], nums[temp] = nums[temp], nums[i]
        
        for i in range(n):
            if i != nums[i] - 1:
                ans.append(nums[i])
        
        return ans
```