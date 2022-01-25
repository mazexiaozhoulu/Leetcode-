# Description
Given a string S of '(' and ')' parentheses, we add the minimum number of parentheses ( '(' or ')', and in any positions ) so that the resulting parentheses string is valid.

Formally, a parentheses string is valid if and only if:

It is the empty string, or
It can be written as AB (A concatenated with B), where A and B are valid strings, or
It can be written as (A), where A is a valid string.
Given a parentheses string, return the minimum number of parentheses we must add to make the resulting string valid.

# Example 1:

Input: "())"
Output: 1

# time

Time Complexity: O(N)O(N), where NN is the length of S.
```
    def minAddToMakeValid(self, S):
        # Write your code here
        left = right = 0
        for i in S:
            if right == 0 and i == ')': 
                # 当前需要增加的右括号数量为0且出现了右括号时，需要增加的左括号数量+1
                left += 1
            else: 
                # 否则如果当前遇到的是左括号，那么需要增加的右括号数量+1，如果遇到的是右括号则-1
                right += 1 if i == '(' else -1
        return left + right
```
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
