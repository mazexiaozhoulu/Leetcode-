```
class Solution:
    """
    @param A: a array
    @return: is it monotonous
    """
    def isMonotonic(self, A):
        # Write your code here.
        if A == sorted(A,reverse=0):
            return True
        elif A == sorted(A,reverse=1):
            return True
        else:
            return False
```
