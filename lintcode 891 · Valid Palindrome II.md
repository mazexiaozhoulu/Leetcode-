
```
class Solution:
    """
    @param s: a string
    @return: whether you can make s a palindrome by deleting at most one character
    """
    def validPalindrome(self, s):
        # Write your code here
        if s is None:
            return True

        left, right = self.diff(s, 0, len(s)-1)
        return self.is_valid(s, left+1, right) or self.is_valid(s, left, right-1)

    def diff(self, s, left, right):
        while left < right:
            if s[left]!= s[right]:
                return left, right
            left += 1
            right -= 1

        return left, right

    def is_valid(self, s, left, right):
        left, right = self.diff(s, left, right)
        return left >= right
```
