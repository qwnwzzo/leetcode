### 542. 01 Matrix

Given a matrix consists of 0 and 1, find the distance of the nearest 0 for each cell.

The distance between two adjacent cells is 1.

**Example 1:**
```
Input:
[[0,0,0],
 [0,1,0],
 [0,0,0]]

Output:
[[0,0,0],
 [0,1,0],
 [0,0,0]]
```

**Example 2:**
```
Input:
[[0,0,0],
 [0,1,0],
 [1,1,1]]

Output:
[[0,0,0],
 [0,1,0],
 [1,2,1]]
```

**Note:**
- The number of elements of the given matrix will not exceed 10,000.
- There are at least one 0 in the given matrix.
- The cells are adjacent in only four directions: up, down, left and right.

**Solution**
```Python
from Queue import Queue

class Solution(object):
    def updateMatrix(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[List[int]]
        """
        if len(matrix) == 0 or len(matrix[0]) == 0:
            return []

        n = len(matrix)
        m = len(matrix[0])
        dist = [[0] * m for _ in range(n)]
        q = Queue()
        for i in range(n):
            for j in range(m):
                if matrix[i][j] == 0:
                    q.put(i * m + j)
                else:
                    dist[i][j] = float("inf")
        
        directions = [0, 1, 0, -1, 0]
        while q.qsize() > 0:
            size = q.qsize()
            cur = q.get()
            row = cur / m
            col = cur % m
            for index in range(4):
                row_temp = row + directions[index]
                col_temp = col + directions[index + 1]
                if row_temp >= 0 and row_temp < n and col_temp >= 0 and col_temp < m:
                    if dist[row_temp][col_temp] > dist[row][col] + 1:
                        dist[row_temp][col_temp] = dist[row][col] + 1
                        q.put(row_temp * m + col_temp)
        
        return dist
```