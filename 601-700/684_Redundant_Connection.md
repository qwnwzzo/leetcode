### 684. Redundant Connection

In this problem, a tree is an undirected graph that is connected and has no cycles.

The given input is a graph that started as a tree with N nodes (with distinct values 1, 2, ..., N), with one additional edge added. The added edge has two different vertices chosen from 1 to N, and was not an edge that already existed.

The resulting graph is given as a 2D-array of edges. Each element of edges is a pair [u, v] with u < v, that represents an undirected edge connecting nodes u and v.

Return an edge that can be removed so that the resulting graph is a tree of N nodes. If there are multiple answers, return the answer that occurs last in the given 2D-array. The answer edge [u, v] should be in the same format, with u < v.

**Example 1:**
```
Input: [[1,2], [1,3], [2,3]]
Output: [2,3]
Explanation: The given undirected graph will be like this:
  1
 / \
2 - 3
```

**Example 2:**
```
Input: [[1,2], [2,3], [3,4], [1,4], [1,5]]
Output: [1,4]
Explanation: The given undirected graph will be like this:
5 - 1 - 2
    |   |
    4 - 3
```

**Note:**
- The size of the input 2D-array will be between 3 and 1000.
- Every integer represented in the 2D-array will be between 1 and N, where N is the size of the input array.

**Solution**
```Python
class UnionFindSet(object):
    def __init__(self, n):
        self.parents = [i for i in range(n + 1)]
        self.ranks = [1 for i in range(n + 1)]
        
    def find(self, u):
        while self.parents[u] != u:
            self.parents[u] = self.parents[self.parents[u]]
            u = self.parents[u]
        
        return u
    
    def union(self, u, v):
        u_root = self.find(u)
        v_root = self.find(v)
        
        if u_root == v_root:
            return False
        
        if self.ranks[u_root] > self.ranks[v_root]:
            self.parents[v_root] = self.parents[u_root]
        elif self.ranks[u_root] < self.ranks[v_root]:
            self.parents[u_root] = self.parents[v_root]
        else:
            self.parents[v_root] = self.parents[u_root]
            self.ranks[u_root] += 1
        
        return True

class Solution(object):
    def findRedundantConnection(self, edges):
        """
        :type edges: List[List[int]]
        :rtype: List[int]
        """
        union_find_set = UnionFindSet(len(edges))
        for e in edges:
            if not union_find_set.union(e[0], e[1]):
                return [e[0], e[1]]
            
        return []
```