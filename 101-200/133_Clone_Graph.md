### 133. Clone Graph

Given a reference of a node in a connected undirected graph, return a deep copy (clone) of the graph. Each node in the graph contains a val (int) and a list (List[Node]) of its neighbors.

**Note:**
- The number of nodes will be between 1 and 100.
- The undirected graph is a simple graph, which means no repeated edges and no self-loops in the graph.
- Since the graph is undirected, if node p has node q as neighbor, then node q must have node p as neighbor too.
- You must return the copy of the given node as a reference to the cloned graph.

**Solution**
```Python
"""
# Definition for a Node.
class Node(object):
    def __init__(self, val, neighbors):
        self.val = val
        self.neighbors = neighbors
"""
class Solution(object):
    def get_all_nodes(self, node):
        queue = [node]
        node_list = set([node])
        
        while len(queue) > 0:
            n = queue.pop(0)
            for neighbour in n.neighbors:
                if neighbour not in node_list:
                    node_list.add(neighbour)
                    queue.append(neighbour)
        
        return list(node_list)
        
    def cloneGraph(self, node):
        """
        :type node: Node
        :rtype: Node
        """
        node_list = self.get_all_nodes(node)
        m = {n: Node(n.val, []) for n in node_list}
        
        for n in m:
            for neighbour in n.neighbors:
                m[n].neighbors.append(m[neighbour])
        
        return m[node]
```