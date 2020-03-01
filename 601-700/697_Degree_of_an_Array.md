### 697. Degree of an Array

Given a non-empty array of non-negative integers `nums`, the **degree** of this array is defined as the maximum frequency of any one of its elements.

Your task is to find the smallest possible length of a (contiguous) subarray of nums, that has the same degree as `nums`.

**Example 1:**
```
Input: [1, 2, 2, 3, 1]
Output: 2
Explanation: 
The input array has a degree of 2 because both elements 1 and 2 appear twice.
Of the subarrays that have the same degree:
[1, 2, 2, 3, 1], [1, 2, 2, 3], [2, 2, 3, 1], [1, 2, 2], [2, 2, 3], [2, 2]
The shortest length is 2. So return 2.
```

**Example 2:**
```
Input: [1,2,2,3,1,4,2]
Output: 6
```

**Note:**
- nums.length will be between 1 and 50,000.
- nums[i] will be an integer between 0 and 49,999.

**Solution**
```Python
class Solution(object):
    def findShortestSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        left_m = {}
        right_m = {}
        count_m = {}
        degree = 0

        for i in range(len(nums)):
            if nums[i] not in left_m:
                left_m[nums[i]] = i
            right_m[nums[i]] = i

            if nums[i] not in count_m:
                count_m[nums[i]] = 0
            count_m[nums[i]] += 1
            degree = max(degree, count_m[nums[i]])
        
        ans = float("inf")
        for num in nums:
            if count_m[num] == degree:
                distance = right_m[num] - left_m[num] + 1
                ans = min(ans, distance)
        
        return ans
```