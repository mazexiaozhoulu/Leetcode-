# Description
Given a string s and a dictionary of words dict, determine if s can be broken into a space-separated sequence of one or more dictionary words.
Because we have used stronger data, the ordinary DFS method can not pass this question now.

# Example 1:

Input:

s = "lintcode"

dict = ["lint", "code"]

Output:

true
# brute force
超时
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
# 记忆化求解
Time complexity O(n^2)
```
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        def canBreak(s, m, wordDict):
            if s in m: return m[s]
            if s in wordDict: 
                m[s] = True
                return True
            
            for i in range(1, len(s)):
                r = s[i:]
                if r in wordDict and canBreak(s[0:i], m, wordDict):
                    m[s] = True
                    return True
            
            m[s] = False
            return False
        return canBreak(s, {}, set(wordDict))

```
