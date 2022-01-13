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
