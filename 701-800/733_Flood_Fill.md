### 733. Flood Fill

To perform a "flood fill", consider the starting pixel, plus any pixels connected 4-directionally to the starting pixel of the same color as the starting pixel, plus any pixels connected 4-directionally to those pixels (also with the same color as the starting pixel), and so on. Replace the color of all of the aforementioned pixels with the newColor.

At the end, return the modified image.

**Example 1:**
```
Input: 
image = [[1,1,1],[1,1,0],[1,0,1]]
sr = 1, sc = 1, newColor = 2
Output: [[2,2,2],[2,2,0],[2,0,1]]
Explanation: 
From the center of the image (with position (sr, sc) = (1, 1)), all pixels connected 
by a path of the same color as the starting pixel are colored with the new color.
Note the bottom corner is not colored 2, because it is not 4-directionally connected
to the starting pixel.
```

**Note:**
- The length of `image` and `image[0]` will be in the range `[1, 50]`.
- The given starting pixel will satisfy `0 <= sr < image.length` and `0 <= sc < image[0]`.length.
- The value of each color in `image[i][j]` and `newColor` will be an integer in `[0, 65535]`.

**Solution**
```Python
class Solution(object):
    def helper(self, image, target, i, j, newColor):
        if i < 0 or i >= len(image) or j < 0 or j >= len(image[0]) or image[i][j] != target:
            return
        
        image[i][j] = newColor
        directions = [0, 1, 0, -1, 0]
        for index in range(4):
            self.helper(image, target, i + directions[index], j + directions[index + 1], newColor)

    def floodFill(self, image, sr, sc, newColor):
        """
        :type image: List[List[int]]
        :type sr: int
        :type sc: int
        :type newColor: int
        :rtype: List[List[int]]
        """
        if len(image) == 0 or len(image[0]) == 0:
            return []
        
        if image[sr][sc] == newColor:
            return image
        
        n = len(image)
        m = len(image[0])
        target = image[sr][sc]
        self.helper(image, target, sr, sc, newColor)

        return image
```