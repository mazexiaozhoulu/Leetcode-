```
class Solution:
    """
    @param s: input string
    @return: a string as the longest palindromic substring
    """
    def longestPalindrome(self, s):
        # write your code here
        palindrome = ''
        for i in range(len(s)):
            len1 = len(self.vaild(i, i, s))

            if len1 > len(palindrome):
                palindrome = self.vaild(i, i, s)

            len2 = len(self.vaild(i, i+1, s))

            if len2 > len(palindrome):
                palindrome = self.vaild(i, i+1, s)
        return palindrome

    def vaild(self, l, r, s):
        while l>=0 and r<len(s) and s[l] == s[r]:
            l -= 1
            r += 1
        return s[l+1: r]
```
