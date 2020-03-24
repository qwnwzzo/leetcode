### 930. Binary Subarrays With Sum

In an array `A` of `0s` and `1s`, how many **non-empty** subarrays have sum S?

**Example 1:**
```
Input: A = [1,0,1,0,1], S = 2
Output: 4
Explanation: 
The 4 subarrays are bolded below:
[1,0,1,0,1]
[1,0,1,0,1]
[1,0,1,0,1]
[1,0,1,0,1]
``` 

**Note:**
- A.length <= 30000
- 0 <= S <= A.length
- A[i] is either 0 or 1.

**Solution**
```Python
class Solution(object):
    def numSubarraysWithSum(self, A, S):
        """
        :type A: List[int]
        :type S: int
        :rtype: int
        """
        pre_sum_arr = [0] * (len(A) + 1)
        for i in range(1, len(pre_sum_arr)):
            pre_sum_arr[i] = pre_sum_arr[i - 1] + A[i - 1]
        
        m = {0: 1}
        ans = 0
        for i in range(1, len(pre_sum_arr)):
            diff = pre_sum_arr[i] - S
            if diff in m:
                ans += m[diff]
            
            if pre_sum_arr[i] not in m:
                m[pre_sum_arr[i]] = 1
            else:
                m[pre_sum_arr[i]] += 1

        return ans
```