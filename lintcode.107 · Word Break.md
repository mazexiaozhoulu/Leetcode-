```
class Solution:
    """
    @param: s: A string
    @param: dict: A dictionary of words dict
    @return: A boolean
    """
    def wordBreak(self, s, dict):
        if not s:
            return True
        for i in range(1,len(s)+1):
            if s[:i] in dict:
                if self.wordBreak(s[i:], dict):
                    return True
        return False
```
