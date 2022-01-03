dict的方法
```
    def singleNumber(self, A):
        # write your code here
        #用dictory 查找：O（1）
        dic = {}
        for i in A:
            dic[i] = dic.get(i, 0) + 1

        for key, value in dic.items():
            if value == 1:
                return key
```
