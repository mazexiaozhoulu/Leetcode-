```
class Solution:
    """
    @param s: the given string s
    @param t: the given string t
    @return: check if s is subsequence of t
    """
    def isSubsequence(self, t, s):
        if not t:
            return True
        index = 0
        for i in range(len(s)):
            if s[i] == t[index]:
                index += 1
                if index >= len(t):
                    break
        return index == len(t)
```
