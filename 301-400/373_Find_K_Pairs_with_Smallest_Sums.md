### 373. Find K Pairs with Smallest Sums

You are given two integer arrays **nums1** and **nums2** sorted in ascending order and an integer **k**.

Define a pair **(u,v)** which consists of one element from the first array and one element from the second array.

Find the k pairs **(u1,v1),(u2,v2) ...(uk,vk)** with the smallest sums.

**Example 1:**
```
Input: nums1 = [1,7,11], nums2 = [2,4,6], k = 3
Output: [[1,2],[1,4],[1,6]] 
Explanation: The first 3 pairs are returned from the sequence: 
             [1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]
```

**Example 2:**
```
Input: nums1 = [1,1,2], nums2 = [1,2,3], k = 2
Output: [1,1],[1,1]
Explanation: The first 2 pairs are returned from the sequence: 
             [1,1],[1,1],[1,2],[2,1],[1,2],[2,2],[1,3],[1,3],[2,3]
```

**Example 3:**
```
Input: nums1 = [1,2], nums2 = [3], k = 3
Output: [1,3],[2,3]
Explanation: All possible pairs are returned from the sequence: [1,3],[2,3]
```

**Solution 01**
```python
from Queue import PriorityQueue

class Solution(object):
    def kSmallestPairs(self, nums1, nums2, k):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :type k: int
        :rtype: List[List[int]]
        """
        q = PriorityQueue()
        for num_1 in nums1:
            for num_2 in nums2:
                q.put([num_1 + num_2, num_1, num_2])
        
        ans = []
        while q.qsize() > 0 and k > 0:
            temp = q.get()
            ans.append([temp[1], temp[2]])
            k -= 1
        
        return ans
```

**Solution 02**
```python
from Queue import PriorityQueue

class Solution(object):
    def kSmallestPairs(self, nums1, nums2, k):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :type k: int
        :rtype: List[List[int]]
        """
        q = PriorityQueue()
        n = len(nums1)
        m = len(nums2)
        for i in range(min(n, k)):
            q.put([nums1[i] + nums2[0], i, 0])
        
        ans = []
        while q.qsize() > 0 and k > 0:
            [_, i, j] = q.get()
            ans.append([nums1[i], nums2[j]])
            k -= 1
            if j + 1 < m:
                q.put([nums1[i] + nums2[j + 1], i, j + 1])
        
        return ans
```