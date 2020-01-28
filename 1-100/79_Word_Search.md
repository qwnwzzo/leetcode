### 79. Word Search

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example:**
```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "ABCCED", return true.
Given word = "SEE", return true.
Given word = "ABCB", return false.
```

**Solution**
```Python
class Solution(object):
    def helper(self, board, word, x, y, start_index):
        if x < 0 or x >= len(board) or y < 0 or y >= len(board[0]) or board[x][y] != word[start_index]:
            return False

        if len(word) - 1 == start_index:
            return board[x][y] == word[start_index]
        
        ans = False
        direction = [0, 1, 0, -1, 0]
        board[x][y] = "#"
        for i in range(4):
            ans = ans or self.helper(board, word, x + direction[i], y + direction[i + 1], start_index + 1)
        board[x][y] = word[start_index]

        return ans

    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        if len(board) == 0 or len(board[0]) == 0 or len(word) == 0:
            return False

        n = len(board)
        m = len(board[0])

        for i in range(n):
            for j in range(m):
                if board[i][j] == word[0] and self.helper(board, word, i, j, 0):
                    return True
        
        return False
```