### 169. Majority Element

Given an array of size n, find the majority element. The majority element is the element that appears **more than** `⌊ n/2 ⌋` times.

You may assume that the array is non-empty and the majority element always exist in the array.

**Example 1:**
```
Input: [3,2,3]
Output: 3
```

**Example 2:**
```
Input: [2,2,1,1,1,2,2]
Output: 2
```

**Solution**
```
class Solution(object):
    def count_range(self, nums, target, lo, hi):
        count = 0
        for i in range(lo, hi + 1):
            if nums[i] == target:
                count += 1
        
        return count
    
    def helper(self, nums, lo, hi):
        if lo == hi:
            return nums[lo]

        mid = lo + (hi - lo) / 2
        left_majority = self.helper(nums, lo, mid)
        right_majority = self.helper(nums, mid + 1, hi)

        if left_majority == right_majority:
            return left_majority
        
        left_majority_count = self.count_range(nums, left_majority, lo, hi)
        right_majority_count = self.count_range(nums, right_majority, lo, hi)

        return left_majority if left_majority_count > right_majority_count else right_majority

    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """

        return self.helper(nums, 0, len(nums) - 1)


class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        ans = 0
        count = 0
        for num in nums:
            if count == 0:
                ans = num
                count += 1
            else:
                if num == ans:
                    count += 1
                else:
                    count -= 1
        
        return ans
```