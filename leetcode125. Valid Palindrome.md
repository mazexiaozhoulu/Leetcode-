```
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        if not s:
            return true
        new = []
        s = s.lower()
        for i in s:
            if i.isalnum():
                new.append(i)
        return new == new[::-1]
```
