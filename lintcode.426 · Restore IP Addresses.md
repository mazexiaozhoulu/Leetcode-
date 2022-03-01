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
        result = []
        self.dfs(s, 0, 0, "", result)
        return result
    def dfs(self, s, pos, dot, t_string, result):
        # 最多加三个点
        if dot > 3:
            return
        # 搜索到最后时
        if pos == len(s):
            if dot == 3:
                nums = t_string.split('.')
                for num in nums:
                    if len(num) > 1 and num[0] == '0':
                        return
                    if int(num) > 255:
                        return
                result.append(t_string)
                return
            return
        
        # pos后不加点的情况
        self.dfs(s, pos + 1, dot, t_string + s[pos], result)
        
        # pos后加点的情况
        if pos < len(s) - 1:
            self.dfs(s, pos + 1, dot + 1, t_string + s[pos] + '.', result)
```
