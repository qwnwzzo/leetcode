### 378. Kth Smallest Element in a Sorted Matrix

Given a n x n matrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.

Note that it is the kth smallest element in the sorted order, not the kth distinct element.

**Example:**
```
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

return 13.
```

**Note:**

You may assume k is always valid, 1 ≤ k ≤ n2.

**Idea**
```
1.找出二维矩阵中最小的数left，最大的数right，那么第k小的数必定在left~right之间
2.mid=(left+right) / 2；在二维矩阵中寻找小于等于mid的元素个数count
3.若这个count小于k，表明第k小的数在右半部分且不包含mid，即left=mid+1, right=right，又保证了第k小的数在left~right之间
4.若这个count大于k，表明第k小的数在左半部分且可能包含mid，即left=left, right=mid，又保证了第k小的数在left~right之间
5.因为每次循环中都保证了第k小的数在left~right之间，当left==right时，第k小的数即被找出，等于right
```

**Solution**
```Python
class Solution(object):
    def find_not_larger_than_mid(self, matrix, mid, row, col):
        # 以列为单位找，找到每一列最后一个<=mid的数即知道每一列有多少个数<=mid
        i = row - 1
        j = 0
        count = 0
        
        while i >= 0 and j < col:
            if matrix[i][j] <= mid:
                # 第j列有i+1个元素<=mid
                count = count + i + 1
                j += 1
            else:
                # 第j列目前的数大于mid，需要继续在当前列往上找
                i -= 1
        
        return count
        
    def kthSmallest(self, matrix, k):
        """
        :type matrix: List[List[int]]
        :type k: int
        :rtype: int
        """
        row = len(matrix)
        col = len(matrix[0])
        left = matrix[0][0]
        right = matrix[-1][-1]
        
        while left < right:
            # 每次循环都保证第K小的数在start~end之间，当start==end，第k小的数就是start
            mid = left + (right - left) / 2
            # 找二维矩阵中<=mid的元素总个数
            count = self.find_not_larger_than_mid(matrix, mid, row, col)
            if count < k:
                # 第k小的数在右半部分，且不包含mid
                left = mid + 1
            else:
                # 第k小的数在左半部分，可能包含mid
                right = mid
        
        return right
```