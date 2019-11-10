### 207. Course Schedule

There are a total of n courses you have to take, labeled from 0 to n-1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

**Example 1:**
```
Input: 2, [[1,0]] 
Output: true
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0. So it is possible.
```

**Example 2:**
```
Input: 2, [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0, and to take course 0 you should
             also have finished course 1. So it is impossible.
```

**Note:**

1. The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.
2. You may assume that there are no duplicate edges in the input prerequisites.

**Solution**
```Python
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        edges = {i: [] for i in range(numCourses)}
        in_degrees = [0 for i in range(numCourses)]
        
        for l in prerequisites:
            edges[l[1]].append(l[0])
            in_degrees[l[0]] += 1
            
        queue = []
        count = 0
        
        for i in range(numCourses):
            if in_degrees[i] == 0:
                queue.append(i)
        
        while len(queue) > 0:
            course = queue.pop(0)
            count += 1
            
            for c in edges[course]:
                in_degrees[c] -= 1
                
                if in_degrees[c] == 0:
                    queue.append(c)
                    
        return numCourses == count
```