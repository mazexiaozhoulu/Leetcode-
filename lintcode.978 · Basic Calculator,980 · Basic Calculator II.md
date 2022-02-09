## Example 1

Input："1 + 1"

Output：2

Example 2

Input："(1+(4+5+2)-3)+(6+8)" 

Output：23

```
class Solution:
    """
    @param s: the given expression
    @return: the result of expression
    """
    def calculate(self, s):
        stack = []
        result = 0
        number = 0
        sign = 1
        for c in s:
            if c in '1234567890':
                number = number * 10 + int(c)
            elif c == '+':
                result += sign * number
                number = 0 
                sign = 1 
            elif c == '-':
                result += sign * number
                number = 0 
                sign = -1 
            elif c == '(':
                stack.append(result)
                stack.append(sign)
                sign = 1
                result = 0
            elif c == ')':
                result += sign * number
                number = 0 
                result *= stack[-1]
                result += stack[-2]
                stack = stack[:-2]
        result += sign * number
        return result
```
## Example
Example 1:

Input:
"3+2*2"
Output:
7
Example 2:

Input:
" 3/2 "
Output:
1

注意：判断符号是为了确保当前符号前的数字和符号后的数字无关，如果有关系就需要pop，无关才能加到stack里
```
class Solution:
    def calculate(self, s: str) -> int:
        stack = []
        num = 0
        preSign = '+'
        
        for i in range(len(s)):
            if s[i].isdigit():
                num = num*10 + int(s[i])
                
            if (not s[i].isdigit() and not s[i].isspace()) or i == len(s)-1:
                if preSign == '+':
                    stack.append(num)
                elif preSign == '-':
                    stack.append(-num)
                elif preSign == '*':
                    stack.append(stack.pop() * num)
                else:
                    stack.append(int(stack.pop() / num))
                preSign = s[i]
                num = 0
        return sum(stack)

    
```
