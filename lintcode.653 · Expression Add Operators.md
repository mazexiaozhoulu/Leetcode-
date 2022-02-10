## Example
Example 1:

Input:
"123"
6
Output: 
["1*2*3","1+2+3"]
Example 2:

Input:
"232"
8
Output: 
["2*3+2", "2+3*2"]

## dfs

每一层递归都进行加减乘除的尝试，回溯
```
class Solution:
    def addOperators(self, num, target):
        def dfs(idx, tmp, tot, last, res):
            if idx == len(num):
                if tot == target:
                    res.append(tmp)
                return
            for i in range(idx, len(num)):
                x = int(num[idx: i + 1])
                if idx == 0:
                    dfs(i + 1, str(x), x, x, res)
                else:
                    dfs(i + 1, tmp + "+" + str(x), tot + x, x, res)
                    dfs(i + 1, tmp + "-" + str(x), tot - x, -x, res)
                    dfs(i + 1, tmp + "*" + str(x), tot - last + last * x, last * x, res)
                if x == 0:
                    break
        res = []
        dfs(0, "", 0, 0, res)
        return res
```
