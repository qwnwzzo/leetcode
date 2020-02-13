### 560. Subarray Sum Equals K

Given an array of integers and an integer **k**, you need to find the total number of continuous subarrays whose sum equals to **k**.

**Example 1:**
```
Input:nums = [1,1,1], k = 2
Output: 2
```

**Note:**
- The length of the array is in range [1, 20,000].
- The range of numbers in the array is [-1000, 1000] and the range of the integer k is [-1e7, 1e7].

**idea**
```
累加数组 + hash table
```

**Solution**
```Python
class Solution(object):
    def subarraySum(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        if len(nums) == 0:
            return 0

        m = {0: 1}
        sum_val = 0
        ans = 0
        for num in nums:
            sum_val += num
            if sum_val - k in m:
                ans += m[sum_val - k]
            
            if sum_val not in m:
                m[sum_val] = 0
            m[sum_val] += 1
        
        return ans
```