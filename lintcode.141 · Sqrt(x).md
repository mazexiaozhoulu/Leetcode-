```
class Solution:
    
    def sqrt(self, square):

        lo, hi = 0, square
        while lo + 1 < hi:
            root = (lo+hi) // 2
            if root > square // root:
                hi = root
            else:
                lo = root
        
        if hi * hi <= square:
            return hi
        return lo
```
