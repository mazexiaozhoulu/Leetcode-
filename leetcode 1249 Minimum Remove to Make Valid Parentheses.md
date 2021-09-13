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
        open = 0
        res = []
        
        for c in s:
		    if c=="(":
			    open+=1
		    elif c==")":
			    if not open:
				    continue
			    open-=1
                
		    res.append(c)
        i = len(res)-1
        while i>=0 and open:
		    if res[i]=="(":
			    res[i]="*"
			    open-=1
		    i-=1
        return "".join([c for c in res if c!="*"])
```
