### 1162. As Far from Land as Possible

Given an N x N grid containing only values 0 and 1, where 0 represents water and 1 represents land, find a water cell such that its distance to the nearest land cell is maximized and return the distance.

The distance used in this problem is the Manhattan distance: the distance between two cells (x0, y0) and (x1, y1) is |x0 - x1| + |y0 - y1|.

If no land or water exists in the grid, return -1.

**Solution**
```Python
class Solution(object):
    def maxDistance(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        n = len(grid)
        m = len(grid[0])
        queue = []
        
        for i in range(n):
            for j in range(m):
                if grid[i][j] == 1:
                    queue.append([i, j])
        
        if len(queue) == n * m or len(queue) == 0:
            return -1
        
        level = 0
        directions = [0, 1, 0, -1, 0]
        
        while len(queue) > 0:
            size = len(queue)
            for i in range(size):
                a, b = queue.pop(0)
                for index in range(4):
                    new_a = a + directions[index]
                    new_b = b + directions[index + 1]
                    if new_a >= 0 and new_a < n and new_b >= 0 and new_b < m and grid[new_a][new_b] == 0:
                        grid[new_a][new_b] = 1
                        queue.append([new_a, new_b])
            
            level += 1
        
        return level - 1
```