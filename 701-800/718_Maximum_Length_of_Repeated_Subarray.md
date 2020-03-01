### 718. Maximum Length of Repeated Subarray

Given two integer arrays `A` and `B`, return the maximum length of an subarray that appears in both arrays.

**Example 1:**
```
Input:
A: [1,2,3,2,1]
B: [3,2,1,4,7]
Output: 3
Explanation: 
The repeated subarray with maximum length is [3, 2, 1].
```

**Note:**
- 1 <= len(A), len(B) <= 1000
- 0 <= A[i], B[i] < 100

**Idea**
```
设 dp[i][j] 为 A[i:] 和 B[j:] 的最长公共前缀，那么答案就为所有 dp[i][j] 中的最大值 
max(dp[i][j])。如果 A[i] == B[j]，那么状态转移方程为 
dp[i][j] = dp[i + 1][j + 1] + 1，
否则状态转移方程为 dp[i][j] = 0。
```

**Solution**
```Python
class Solution(object):
    def findLength(self, A, B):
        """
        :type A: List[int]
        :type B: List[int]
        :rtype: int
        """
        n = len(A)
        m = len(B)
        dp = [[0] * (m + 1) for _ in range(n + 1)]
        for i in range(n - 1, -1, -1):
            for j in range(m - 1, -1, -1):
                if A[i] == B[j]:
                    dp[i][j] = dp[i + 1][j + 1] + 1
        
        return max([max(l) for l in dp])
```