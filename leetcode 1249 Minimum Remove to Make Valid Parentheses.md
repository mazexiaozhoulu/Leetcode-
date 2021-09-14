 两个部分：
      
找balance的括号
        
删掉多余的再把剩下的字符放到一起

想法，用stack，属于字母的先放进去，属于括号的，左括号+1，右括号-1（如果balance = 0，那么直接跳过这个），并且把括号放进去。看balance的值
        
开始pop出来字符，如果stack有值并且balance>=0,说明左括号多了，要把做括号去掉。这里我们用*表示做括号的位置，之后碰到*号就join起来其他字符。再把balance-1
```
class Solution(object):
    def minRemoveToMakeValid(self, s):
        """
        :type s: str
        :rtype: str
        """
        balance = 0
        stack = []
        
        for i in s:
            if i == "(":
                balance += 1
            elif i == ")":
                if not balance:
                    continue
                else:
                    balance -= 1
            stack.append(i)
	    
        for j in range(-1, -len(stack)-1, -1):
            if balance > 0:
                if stack[j] == "(":
                    stack[j] = "*"
                    balance -= 1
                        
        return "".join([j for j in stack if j!="*"])
```
