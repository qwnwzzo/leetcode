### 721. Accounts Merge

Given a list accounts, each element accounts[i] is a list of strings, where the first element accounts[i][0] is a name, and the rest of the elements are emails representing emails of the account.

Now, we would like to merge these accounts. Two accounts definitely belong to the same person if there is some email that is common to both accounts. Note that even if two accounts have the same name, they may belong to different people as people could have the same name. A person can have any number of accounts initially, but all of their accounts definitely have the same name.

After merging the accounts, return the accounts in the following format: the first element of each account is the name, and the rest of the elements are emails **in sorted order**. The accounts themselves can be returned in any order.

**Example 1:**
```
Input: 
accounts = [["John", "johnsmith@mail.com", "john00@mail.com"], ["John", "johnnybravo@mail.com"], ["John", "johnsmith@mail.com", "john_newyork@mail.com"], ["Mary", "mary@mail.com"]]

Output: 
[["John", 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com'],  ["John", "johnnybravo@mail.com"], ["Mary", "mary@mail.com"]]

Explanation: 
The first and third John's are the same person as they have the common email "johnsmith@mail.com".
The second John and Mary are different people as none of their email addresses are used by other accounts.
We could return these lists in any order, for example the answer [['Mary', 'mary@mail.com'], ['John', 'johnnybravo@mail.com'], 
['John', 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com']] would still be accepted.
```

**Note:**

- The length of accounts will be in the range [1, 1000].
- The length of accounts[i] will be in the range [1, 10].
- The length of accounts[i][j] will be in the range [1, 30].

**Solution**
```Python
class UnionFindSet(object):
    def __init__(self):
        self.parents = {}
        
    def find(self, u):
        if u not in self.parents:
            self.parents[u] = u
            return u
        
        while self.parents[u] != u:
            self.parents[u] = self.parents[self.parents[u]]
            u = self.parents[u]
        
        return u
    
    def union(self, u, v):
        u_root = self.find(u)
        v_root = self.find(v)
        
        if u_root == v_root:
            return False
        
        self.parents[v_root] = u_root
        
        return True
    
class Solution(object):
    def accountsMerge(self, accounts):
        """
        :type accounts: List[List[str]]
        :rtype: List[List[str]]
        """
        union_find_set = UnionFindSet()
        email_to_name = {}
        for l in accounts:
            name = l[0]
            for email in l[1:]:
                if email not in email_to_name:
                    email_to_name[email] = name
                
                union_find_set.union(l[1], email)
        
        m = {}
        for email in email_to_name:
            root = union_find_set.find(email)
            if root not in m:
                m[root] = []
            m[root].append(email)
        
        ans = []
        for email in m:
            ans.append([email_to_name[email]] + sorted(m[email]))
            
        return ans
```