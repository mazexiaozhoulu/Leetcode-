```
    def myPow(self, x: float, n: int) -> float:       
        if n == 0:
            return 1
        
        if n < 0:
            x = 1 / x
            n = -n
        
        if n % 2 == 1:
            return x * self.myPow(x**2, (n - 1) / 2)
        else:
            return self.myPow(x**2, n / 2)

```
