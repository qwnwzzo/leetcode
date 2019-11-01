### 737. Sentence Similarity II

Given two sentences words1, words2 (each represented as an array of strings), and a list of similar word pairs pairs, determine if two sentences are similar.

For example, `words1 = ["great", "acting", "skills"]` and `words2 = ["fine", "drama", "talent"]` are similar, if the similar word pairs are `pairs = [["great", "good"], ["fine", "good"], ["acting","drama"], ["skills","talent"]]`.

Note that the similarity relation is transitive. For example, if "great" and "good" are similar, and "fine" and "good" are similar, then "great" and "fine" **are similar**.

Similarity is also symmetric. For example, "great" and "fine" being similar is the same as "fine" and "great" being similar.

Also, a word is always similar with itself. For example, the sentences `words1 = ["great"], words2 = ["great"], pairs = []` are similar, even though there are no specified similar word pairs.

Finally, sentences can only be similar if they have the same number of words. So a sentence like `words1 = ["great"]` can never be similar to `words2 = ["doubleplus","good"]`.

**Note:**

The length of words1 and words2 will not exceed 1000.
The length of pairs will not exceed 2000.
The length of each pairs[i] will be 2.
The length of each words[i] and pairs[i][j] will be in the range [1, 20].

**Solution**
```Python
class UnionFindSet(object):
    def __init__(self, pairs):
        self.parents = {}
        self.ranks = {}
        for l in pairs:
            self.parents[l[0]] = l[0]
            self.parents[l[1]] = l[1]
            self.ranks[l[0]] = 1
            self.ranks[l[1]] = 1
    
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
    def areSentencesSimilarTwo(self, words1, words2, pairs):
        """
        :type words1: List[str]
        :type words2: List[str]
        :type pairs: List[List[str]]
        :rtype: bool
        """
        if len(words1) != len(words2):
            return False
        
        union_find_set = UnionFindSet(pairs)
        for l in pairs:
            union_find_set.union(l[0], l[1])
        
        for i in range(len(words1)):
            if words1[i] == words2[i]:
                continue
            else:
                if words1[i] not in union_find_set.parents or words2[i] not in union_find_set.parents:
                    return False
                
                u = union_find_set.find(words1[i])
                v = union_find_set.find(words2[i])
                if u != v:
                    return False
        
        return True
```