### 130. Surrounded Regions

Given a 2D board containing `'X'` and `'O'` (**the letter O**), capture all regions surrounded by 'X'.

A region is captured by flipping all `'O's` into `'X's` in that surrounded region.

**Example:**
```
X X X X
X O O X
X X O X
X O X X
After running your function, the board should be:

X X X X
X X X X
X X X X
X O X X

Explanation:

Surrounded regions shouldn’t be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.
```

**Solution**
```Python
class Solution(object):
    def helper(self, board, x, y):
        n = len(board)
        m = len(board[0])
        if x < 0 or x >= n or y < 0 or y >= m or board[x][y] == "#" or board[x][y] == "X":
            return

        board[x][y] = "#"
        d = [0, 1, 0, -1, 0]
        for i in range(4):
            self.helper(board, x + d[i], y + d[i + 1])

    def solve(self, board):
        """
        :type board: List[List[str]]
        :rtype: None Do not return anything, modify board in-place instead.
        """
        starting_points = []
        for i in range(len(board)):
            for j in range(len(board[0])):
                if i == 0 or i == len(board) - 1 or j == 0 or j == len(board[0]) - 1:
                    if board[i][j] == "O":
                        starting_points.append([i, j])

        for point in starting_points:
            self.helper(board, point[0], point[1])

        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] == "#":
                    board[i][j] = "O"
                elif board[i][j] == "O":
                    board[i][j] = "X"
```