### 925. Long Pressed Name

Your friend is typing his `name` into a keyboard.  Sometimes, when typing a character `c`, the key might get long pressed, and the character will be typed 1 or more times.

You examine the `typed` characters of the keyboard.  Return `True` if it is possible that it was your friends name, with some characters (possibly none) being long pressed.

 
Example 1:

Input: name = "alex", typed = "aaleex"
Output: true
Explanation: 'a' and 'e' in 'alex' were long pressed.


**Example 2:**
```
Input: name = "saeed", typed = "ssaaedd"
Output: false
Explanation: 'e' must have been pressed twice, but it wasn't in the typed output.
```

**Example 3:**
```
Input: name = "leelee", typed = "lleeelee"
Output: true
```

**Example 4:**
```
Input: name = "laiden", typed = "laiden"
Output: true
Explanation: It's not necessary to long press any character.
```

**Note:**
- name.length <= 1000
- typed.length <= 1000
- The characters of name and typed are lowercase letters.

**Solution**
```Python
class Solution(object):
    def isLongPressedName(self, name, typed):
        """
        :type name: str
        :type typed: str
        :rtype: bool
        """
        name_index = 0
        typed_index = 0

        while name_index < len(name):
            if typed_index == len(typed):
                break

            if name[name_index] == typed[typed_index]:
                name_index += 1
                typed_index += 1
            else:
                while typed_index < len(typed) and name[name_index] != typed[typed_index]:
                    typed_index += 1

        if name_index != len(name):
            return False
        
        if len(typed) > 1:
            c = typed[typed_index - 1]
            for i in range(typed_index, len(typed)):
                if typed[i] != c:
                    return False
        
        return True
```