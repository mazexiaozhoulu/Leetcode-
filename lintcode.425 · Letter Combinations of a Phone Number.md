backtracking 
```
    def letterCombinations(self, digits):
        if not digits:
            return []
        # write your code here
        phone = {'2':['a','b','c'],
                 '3':['d','e','f'],
                 '4':['g','h','i'],
                 '5':['j','k','l'],
                 '6':['m','n','o'],
                 '7':['p','q','r','s'],
                 '8':['t','u','v'],
                 '9':['w','x','y','z']}
        res = []
        self.backtracking('', digits, res, phone)
        return res

    def backtracking(self, combination, nextdigit, res, phone):
        if len(nextdigit) == 0:
            return res.append(combination)
        else:
            for letter in phone[nextdigit[0]]:
                self.backtracking(combination + letter, nextdigit[1:], res, phone)

```
