```
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        if not s:
            return true
        new = []
        s = s.lower()
        for i in s:
            if i.isalnum():
                new.append(i)
        return new == new[::-1]
```
注意区别
        print new
        print new.reverse() 是inplace的，返回值是None
        print reversed(new) 返回值是翻转后的list，且改变不是inplace的, 并且显示的是reference
        print list(reversed(new))要用list把它显示出来
