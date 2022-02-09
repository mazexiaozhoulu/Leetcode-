## Description
Given a string containing only digits, restore it by returning all possible valid IP address combinations.

(Your task is to add three dots to this string to make it a valid IP address. Return all possible IP address.)

##Example
Example 1:

Input: "25525511135"

Output: ["255.255.11.135", "255.255.111.35"]

Explanation: ["255.255.111.35", "255.255.11.135"] will be accepted as well.

## 方法 dfs 、
时间复杂度 2^n
```
class Solution:
    """
    @param s: the IP string
    @return: All possible valid IP addresses
    """
    def restoreIpAddresses(self, s):
        path = []
        result = []
        self.dfs(s, path, result)
        return result
    
    def dfs(self, s, path,result):
        
        if not s and len(path) == 4:
            s = '.'.join(path[::-1])
            result.append(s)
            return
        elif len(path) == 4: 
            return 
        else:
            for i in range(1, min(3, len(s))+1):
                if int(s[:i]) >= 0 and int(s[:i]) <= 255:
                    if i > 1 and s[0]=='0': continue
                    else: self.dfs(s[i:], [s[:i]]+path, result)
            return
```
