# Description
Given a string s and a dictionary of words dict, add spaces in s to construct a sentence where each word is a valid dictionary word.

Return all such possible sentences.

# sample

Input："lintcode"，["de","ding","co","code","lint"]

Output：["lint code", "lint co de"]

Explanation：

insert a space is "lint code"，insert two spaces is "lint co de".
# 记忆化求解 o(2^n)
```
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
        words = set(wordDict)
        mem = {}
        #记忆话求解
        def wordBreak(s):
            if s in mem: 
                return mem[s]
            ans = []
            if s in words: 
                ans.append(s)
            
            for i in range(1, len(s)):
                right = s[i:]
                if right not in words: 
                    continue      
                #如果有解的话，就合起来
                ans += [w + " " + right for w in wordBreak(s[0:i])]
            mem[s] = ans
            return mem[s]
        return wordBreak(s)
```
