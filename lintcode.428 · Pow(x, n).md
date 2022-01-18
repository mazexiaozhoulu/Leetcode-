不论我们返回时候如何，我们执行第一步，先设立Base Case:

if b == 0: return 1

完了以后，我们要对大问题进行拆分，也就是不断的对b的值折半

拆分：

half = self.myPow(a, b // 2)

当拆分到了最小的问题，满足base case b == 0 的时候，我们则进行返回，返回时候有三种可能

Function的三种可能性：

>当b为偶数的时候，比如 2 ^ 100，拆分的时候就变成 (2 ^ 50) * (2 ^ 50)

>当b为基数的时候，比如 2 ^ 25，拆分的时候就变成 (2 ^12) * (2 ^ 12) * 2

>当b为负数的时候，返回 1.0 / self.myPow(a, -b)
>
```
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n < 0:
            return 1/self.helper(x, -n)
        else:
            return self.helper(x, n)
        
    def helper(self, x, n):
        if n == 0:
            return 1
        half = self.helper(x, n//2) # 直到return 1 附值给half，然后才能进行下一步
        if n % 2 == 0:
            return half * half
        else:
            return half * half * x
```
