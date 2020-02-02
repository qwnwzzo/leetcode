### 221. Maximal Square

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

**Example:**
```
Input: 

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

Output: 4
```

**Solution**
```Python
class Solution(object):
    def maximalSquare(self, matrix):
        """
        :type matrix: List[List[str]]
        :rtype: int
        """
        if len(matrix) == 0 or len(matrix[0]) == 0:
            return 0

        ans = 0
        n = len(matrix)
        m = len(matrix[0])
        dp = [[0 for j in range(m)] for i in range(n)]

        for j in range(m):
            if matrix[0][j] == "1":
                ans = 1
                dp[0][j] = 1
        
        for i in range(n):
            if matrix[i][0] == "1":
                ans = 1
                dp[i][0] = 1
        
        for i in range(1, n):
            for j in range(1, m):
                if matrix[i][j] == "1":
                    dp[i][j] = min(dp[i][j - 1], dp[i - 1][j], dp[i - 1][j - 1]) + 1
                    ans = max(ans, dp[i][j])
        
        return ans * ans
```