```
class Solution:
    def longestValidParentheses(self, s):
        stack = []
        result = 0

        for i in range(len(s)):
          if s[i] == "(":
            stack.append(i)
          elif stack and s[stack[-1]] == "(":
            stack.pop()
            last_index = stack[-1] if stack else -1
            result = max(result, i - last_index)
          else:
            stack.append(i)

        return result
```
