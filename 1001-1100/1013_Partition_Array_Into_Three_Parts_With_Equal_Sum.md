### 1013. Partition Array Into Three Parts With Equal Sum

Given an array A of integers, return true if and only if we can partition the array into three **non-empty** parts with equal sums.

Formally, we can partition the array if we can find indexes `i+1 < j` with `(A[0] + A[1] + ... + A[i] == A[i+1] + A[i+2] + ... + A[j-1] == A[j] + A[j-1] + ... + A[A.length - 1])`

 

**Example 1:**
```
Input: A = [0,2,1,-6,6,-7,9,1,2,0,1]
Output: true
Explanation: 0 + 2 + 1 = -6 + 6 - 7 + 9 + 1 = 2 + 0 + 1
```

**Example 2:**
```
Input: A = [0,2,1,-6,6,7,9,-1,2,0,1]
Output: false
```

**Example 3:**
```
Input: A = [3,3,6,5,-2,2,5,1,-9,4]
Output: true
Explanation: 3 + 3 = 6 = 5 - 2 + 2 + 5 + 1 - 9 + 4
```

**Constraints:**
- 3 <= A.length <= 50000
- -10^4 <= A[i] <= 10^4

**Solution**
```Python
class Solution(object):
    def canThreePartsEqualSum(self, A):
        """
        :type A: List[int]
        :rtype: bool
        """
        if len(A) < 3:
            return False
        
        sum_num = sum(A)
        if sum_num % 3 != 0:
            return False
        
        interval = sum_num / 3
        find_first = False
        find_second = False
        temp_sum = 0
        for i in range(len(A) - 1):
            temp_sum += A[i]
            if not find_first and temp_sum == interval:
                find_first = True
            elif find_first and not find_second and temp_sum == interval * 2:
                find_second = True
        
        return find_first and find_second
```