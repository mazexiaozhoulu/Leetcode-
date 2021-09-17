two point
```
class Solution:
    """
    @param s: string S
    @param t: string T
    @return: whether S can convert to T
    """
    def canConvert(self, s, t):
        # Write your code here
        if not s:
            return False
        if not t:
            return True

        spoint = 0
        tpoint = 0
        while spoint < len(s) and tpoint < len(t):
            if s[spoint] == t[tpoint]:
                spoint += 1
                tpoint += 1
            else:
                spoint += 1

        return tpoint == len(t)
        
```
