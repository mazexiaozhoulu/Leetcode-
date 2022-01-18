```
class Solution:
    def addBinary(self, a, b) -> str:
        return '{0:b}'.format(int(a, 2) + int(b, 2))
```
'b' - 二进制。将数字以2为基数进行输出。

int(a,2)是把a改成二进制
