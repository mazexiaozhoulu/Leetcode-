## Description
A message containing letters from A-Z is being encoded to numbers using the following mapping:

'A' -> 1
'B' -> 2
...
'Z' -> 26
Given an encoded message containing digits, determine the total number of ways to decode it.

## Example
Example 1:

Input: "12"
Output: 2
Explanation: It could be decoded as AB (1 2) or L (12).

## 方法 dfs memorize
```
class Solution:
    """
    @param s: a string,  encoded message
    @return: an integer, the number of ways decoding
    """
    def numDecodings(self, s):
        # write your code here
        
        if not s:
            
            return 0
        
        return self.dfs(s, 0, {})
        
    def dfs(self, s, start_index, memo):
        
        if start_index in memo:
            
            return memo[start_index]
            
        if start_index == len(s):
            
            return 1
        
        if s[start_index] == '0':
            
            return 0 
    
        result = self.dfs(s, start_index + 1, memo)
        
        if  start_index + 2 <= len(s)  and int(s[start_index : start_index + 2]) <= 26:
            
            result += self.dfs(s, start_index + 2, memo)
            
        memo[start_index] = result 
        
        return result
```
