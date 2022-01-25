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
        # m是memory，一个dict。检查s在不在memory里，在的话就直接返回，不需要重复求解
            if s in m: return m[s]
        # 如果整个s都在worddict里，整个字符串标记为True
            if s in wordDict: 
                m[s] = True
                return True
           #尝试分割点，一部分左边，一部分右边
            for i in range(1, len(s)):
                r = s[i:]
            #如果右半部分在字典里，并且左半部分有解，记下来，直接return
                if r in wordDict and canBreak(s[0:i], m, wordDict):
                    m[s] = True
                    return True
            
            m[s] = False
            return False
        return canBreak(s, {}, set(wordDict))

```
