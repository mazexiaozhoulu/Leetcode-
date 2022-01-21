```
class Solution:
    """
    @param S: the given string
    @return: the minimum number of parentheses we must add
    """
    def minAddToMakeValid(self, S):
        # Write your code here
        stack = []
        for i in S:
            if i == ")" and stack and stack[-1] == "(":
                stack.pop()
            else:
                stack.append(i)

        return len(stack)
```
