### 200. Number of Islands

Given a 2d grid map of `'1's` (land) and `'0's` (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**
```
Input:
11110
11010
11000
00000

Output: 1
```

**Example 2:**
```
Input:
11000
11000
00100
00011

Output: 3
```

**Solution**
```Python
class Solution(object):
    def helper(self, grid, x, y):
        if x < 0 or x >= len(grid) or y < 0 or y >= len(grid[0]) or grid[x][y] == "0":
            return
        
        grid[x][y] = "0"
        directions = [0, 1, 0, -1, 0]
        for i in range(4):
            self.helper(grid, x + directions[i], y + directions[i + 1])

    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        if len(grid) == 0 or len(grid[0]) == 0:
            return 0
            
        n = len(grid)
        m = len(grid[0])
        count = 0

        for i in range(n):
            for j in range(m):
                if grid[i][j] == "1":
                    count += 1
                    self.helper(grid, i, j)
        
        return count
```