### 990. Satisfiability of Equality Equations

Given an array equations of strings that represent relationships between variables, each string equations[i] has length 4 and takes one of two different forms: "a==b" or "a!=b".  Here, a and b are lowercase letters (not necessarily different) that represent one-letter variable names.

Return true if and only if it is possible to assign integers to variable names so as to satisfy all the given equations.

**Example 1:**
```
Input: ["a==b","b!=a"]
Output: false
Explanation: If we assign say, a = 1 and b = 1, then the first equation is satisfied, but not the second.  There is no way to assign the variables to satisfy both equations.
```

**Example 2:**
```
Input: ["b==a","a==b"]
Output: true
Explanation: We could assign a = 1 and b = 1 to satisfy both equations.
```

**Example 3:**
```
Input: ["a==b","b==c","a==c"]
Output: true
```

**Example 4:**
```
Input: ["a==b","b!=c","c==a"]
Output: false
```

**Example 5:**
```
Input: ["c==c","b==d","x!=z"]
Output: true
```

**Note:**
- 1 <= equations.length <= 500
- equations[i].length == 4
- equations[i][0] and equations[i][3] are lowercase letters
- equations[i][1] is either '=' or '!'
- equations[i][2] is '='

**Idea**
```
先处理相等的情况，把相等的Union起来。
然后对比不相等的，如果不相等的有相同的root节点，则return false。
最后return true
```

**Solution**
```Python
class UnionFindSet(object):
    def __init__(self):
        self.parents = {}
        self.ranks = {}
        
    def find(self, u):
        if u not in self.parents:
            self.parents[u] = u
            self.ranks[u] = 1
        
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
    def equationsPossible(self, equations):
        """
        :type equations: List[str]
        :rtype: bool
        """
        union_find_set = UnionFindSet()
        for e in equations:
            if e[1: 3] == "==":
                union_find_set.union(e[0], e[3])
        
        for e in equations:
            if e[1: 3] == "!=":
                a_root = union_find_set.find(e[0])
                b_root = union_find_set.find(e[3])
                if a_root == b_root:
                    return False
        
        return True
```