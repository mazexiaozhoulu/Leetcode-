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
            #phone[nextdigit[0]] 表示的是 nextdigit[1:]的第一个数字，如果sample是2345，那第一次就是2345的2，第二次是345的3，第三次是45的4
                self.backtracking(combination + letter, nextdigit[1:], res, phone)

```
