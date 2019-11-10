### 323. Number of Connected Components in an Undirected Graph

Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to find the number of connected components in an undirected graph.

**Example 1:**
```
Input: n = 5 and edges = [[0, 1], [1, 2], [3, 4]]

     0          3
     |          |
     1 --- 2    4 

Output: 2
```

**Example 2:**
```
Input: n = 5 and edges = [[0, 1], [1, 2], [2, 3], [3, 4]]

     0           4
     |           |
     1 --- 2 --- 3

Output:  1
```

**Note:**
You can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.

**Solution**
```Python
class Solution(object):
    def helper(self, graph, marks, v):
        marks[v] = True
        for neighbour in graph[v]:
            if not marks[neighbour]:
                self.helper(graph, marks, neighbour)
        
    def countComponents(self, n, edges):
        """
        :type n: int
        :type edges: List[List[int]]
        :rtype: int
        """
        count = 0
        marks = [False for i in range(n)]
        graph = {i: [] for i in range(n)}
        for e in edges:
            graph[e[0]].append(e[1])
            graph[e[1]].append(e[0])
        
        for i in range(n):
            if not marks[i]:
                self.helper(graph, marks, i)
                count += 1
                
        return count
```