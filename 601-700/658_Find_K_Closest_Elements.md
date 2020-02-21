### 658. Find K Closest Elements

Given a sorted array, two integers `k` and `x`, find the `k` closest elements to `x` in the array. The result should also be sorted in ascending order. If there is a tie, the smaller elements are always preferred.

**Example 1:**
```
Input: [1,2,3,4,5], k=4, x=3
Output: [1,2,3,4]
```

**Example 2:**
```
Input: [1,2,3,4,5], k=4, x=-1
Output: [1,2,3,4]
```

**Solution**
```Python
class Solution(object):
    def find_index(self, arr, x):
        start = 0
        end = len(arr) - 1
        while start + 1 < end:
            mid = start + (end - start) / 2
            if arr[mid] < x:
                start = mid
            else:
                end = mid
        
        if arr[start] >= x:
            return start
        
        return end
        
    def findClosestElements(self, arr, k, x):
        """
        :type arr: List[int]
        :type k: int
        :type x: int
        :rtype: List[int]
        """
        if k > len(arr):
            return arr
        
        if x <= arr[0]:
            return arr[: k]
        
        if x >= arr[-1]:
            return arr[len(arr) - k:]
        
        index = self.find_index(arr, x)
        start = index - 1
        end = index
        ans = []
        
        for i in range(k):
            if start < 0:
                ans.append(arr[end])
                end += 1
            elif end >= len(arr):
                ans = [arr[start]] + ans
                start -= 1
            else:
                if abs(x - arr[start]) <= abs(x - arr[end]):
                    ans = [arr[start]] + ans
                    start -= 1
                else:
                    ans.append(arr[end])
                    end += 1
        
        return ans
```