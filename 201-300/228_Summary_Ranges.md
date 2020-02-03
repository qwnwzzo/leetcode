### 228. Summary Ranges

Given a sorted integer array without duplicates, return the summary of its ranges.

**Example 1:**
```
Input:  [0,1,2,4,5,7]
Output: ["0->2","4->5","7"]
Explanation: 0,1,2 form a continuous range; 4,5 form a continuous range.
```

**Example 2:**
```
Input:  [0,2,3,4,6,8,9]
Output: ["0","2->4","6","8->9"]
Explanation: 2,3,4 form a continuous range; 8,9 form a continuous range.
```

**Solution**
```Python
class Solution(object):
    def summaryRanges(self, nums):
        """
        :type nums: List[int]
        :rtype: List[str]
        """
        if len(nums) == 0:
            return []

        ans = []
        left = 0
        for i in range(len(nums)):
            if i == left:
                ans.append(str(nums[i]))
                if i < len(nums) - 1 and nums[i] + 1 < nums[i + 1]:
                    left = i + 1
            elif i < len(nums) - 1 and nums[i] + 1 == nums[i + 1]:
                continue
            elif i < len(nums) - 1 and nums[i] + 1 < nums[i + 1]:
                left = i + 1
                ans[-1] = ans[-1] + "->" + str(nums[i])
            else:
                ans[-1] = ans[-1] + "->" + str(nums[i])
        
        return ans
        
        return ans
```