### 705. Design HashSet

Design a HashSet without using any built-in hash table libraries.

To be specific, your design should include these functions:
- `add(value):` Insert a value into the HashSet. 
- `contains(value):` Return whether the value exists in the HashSet or not.
- `remove(value):` Remove a value in the HashSet. If the value does not exist in the HashSet, do nothing.

**Example:**
```
MyHashSet hashSet = new MyHashSet();
hashSet.add(1);         
hashSet.add(2);         
hashSet.contains(1);    // returns true
hashSet.contains(3);    // returns false (not found)
hashSet.add(2);          
hashSet.contains(2);    // returns true
hashSet.remove(2);          
hashSet.contains(2);    // returns false (already removed)
```

**Note:**
- All values will be in the range of [0, 1000000].
- The number of operations will be in the range of [1, 10000].
- Please do not use the built-in HashSet library.

**Solution**
```Python
class Node(object):
    def __init__(self, val):
        self.val = val
        self.next = None
    
class Bucket(object):
    def __init__(self):
        self.head = Node(0)
    
    def contains(self, val):
        cur = self.head
        while cur.next is not None:
            if cur.next.val == val:
                return True
            cur = cur.next
        
        return False
    
    def add(self, val):
        if not self.contains(val):
            temp = self.head.next
            n = Node(val)
            self.head.next = n
            n.next = temp
    
    def remove(self, val):
        if self.contains(val):
            cur = self.head
            while cur.next.val != val:
                cur = cur.next

            cur.next = cur.next.next

class MyHashSet(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.key_range = 769
        self.bucket_arr = [Bucket() for _ in range(self.key_range)]
    
    def _hash_func(self, val):
        return val % self.key_range

    def add(self, key):
        """
        :type key: int
        :rtype: None
        """
        if not self.contains(key):
            hash_val = self._hash_func(key)
            self.bucket_arr[hash_val].add(key)

    def remove(self, key):
        """
        :type key: int
        :rtype: None
        """
        if self.contains(key):
            hash_val = self._hash_func(key)
            self.bucket_arr[hash_val].remove(key)

    def contains(self, key):
        """
        Returns true if this set contains the specified element
        :type key: int
        :rtype: bool
        """
        hash_val = self._hash_func(key)
        return self.bucket_arr[hash_val].contains(key)


# Your MyHashSet object will be instantiated and called as such:
# obj = MyHashSet()
# obj.add(key)
# obj.remove(key)
# param_3 = obj.contains(key)
```