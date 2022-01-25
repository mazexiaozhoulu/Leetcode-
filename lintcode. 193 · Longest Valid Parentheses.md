# Description
Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

# Example
Example 1:

Input: "(()"

Output: 2

Explanation: The longest valid parentheses substring is "()"

# TIME
Time complexity: O(n)O(n). nn is the length of the given string.

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
