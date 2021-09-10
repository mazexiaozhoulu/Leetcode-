注意 ch == ""
注意最后吧stack里内容pop出去后要reverse

```
class Solution(object):
    def simplifyPath(self, path):
        """
        :type path: str
        :rtype: str
        """
        path = path.split('/')
        stack = []
        for ch in path:
            if ch == "." or ch == "":
                continue
            elif ch == "..":
                if stack:
                    stack.pop()
            else:
                stack.append(ch)
                
        if not stack:
            return '/'
        
        strs = ''
        while stack:
            strs = '/'+ stack.pop() + strs
        return strs
```
