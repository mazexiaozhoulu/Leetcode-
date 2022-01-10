```
class Solution:
    def countAndSay(self, n):
        res = "1"
        if n == 1:
            return res
        
        for i in range(2, n+1):
            l, r = 0, 0
            
            temp = ""
            # 外层while控制循环完这一层的数字，如"1211"
            while r < len(res):
                # 这层while控制把相同的数字都遍历完
                while r < len(res) and res[l] == res[r]:
                    r += 1

                curr_len = r - l
                temp += str(curr_len) + res[l]
                l = r
            
            res = temp
        
        return res
```
