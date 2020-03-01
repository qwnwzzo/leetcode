### 706. Design HashMap

Design a HashMap without using any built-in hash table libraries.

To be specific, your design should include these functions:
- `put(key, value):` Insert a (key, value) pair into the HashMap. If the value already exists in the HashMap, update the value.
- `get(key):` Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key.
- `remove(key):` Remove the mapping for the value key if this map contains the mapping for the key.

**Example:**
```
MyHashMap hashMap = new MyHashMap();
hashMap.put(1, 1);          
hashMap.put(2, 2);         
hashMap.get(1);            // returns 1
hashMap.get(3);            // returns -1 (not found)
hashMap.put(2, 1);          // update the existing value
hashMap.get(2);            // returns 1 
hashMap.remove(2);          // remove the mapping for 2
hashMap.get(2);            // returns -1 (not found) 
```

**Note:**
- All keys and values will be in the range of [0, 1000000].
- The number of operations will be in the range of [1, 10000].
- Please do not use the built-in HashMap library.

**Solution**
```Python
class Node(object):
    def __init__(self, key, val):
        self.key = key
        self.val = val
        self.next = None

class Bucket(object):
    def __init__(self):
        self.head = Node(None, None)
    
    def contains(self, key):
        cur = self.head
        while cur.next is not None:
            if cur.next.key == key:
                return True

            cur = cur.next
        
        return False
    
    def get(self, key):
        if not self.contains(key):
            return -1
        
        cur = self.head
        while cur.next.key != key:
            cur = cur.next
        
        return cur.next.val
    
    def put(self, key, val):
        if not self.contains(key):
            temp = self.head.next
            n = Node(key, val)
            self.head.next = n
            n.next = temp
        else:
            cur = self.head
            while cur.next.key != key:
                cur = cur.next
            cur.next.val = val
    
    def remove(self, key):
        if self.contains(key):
            cur = self.head
            while cur.next.key != key:
                cur = cur.next
            cur.next = cur.next.next

class MyHashMap(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.key_range = 697
        self.bucket_arr = [Bucket() for _ in range(self.key_range)]
    
    def _hash_func(self, key):
        return key % self.key_range

    def put(self, key, value):
        """
        value will always be non-negative.
        :type key: int
        :type value: int
        :rtype: None
        """
        hash_val = self._hash_func(key)
        self.bucket_arr[hash_val].put(key, value)

    def get(self, key):
        """
        Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key
        :type key: int
        :rtype: int
        """
        hash_val = self._hash_func(key)
        return self.bucket_arr[hash_val].get(key)

    def remove(self, key):
        """
        Removes the mapping of the specified value key if this map contains a mapping for the key
        :type key: int
        :rtype: None
        """
        hash_val = self._hash_func(key)
        self.bucket_arr[hash_val].remove(key)

# Your MyHashMap object will be instantiated and called as such:
# obj = MyHashMap()
# obj.put(key,value)
# param_2 = obj.get(key)
# obj.remove(key)
```