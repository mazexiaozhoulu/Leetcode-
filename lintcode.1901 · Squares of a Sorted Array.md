```
from typing import (
    List,
)

class Solution:
    """
    @param A: The array A.
    @return: The array of the squares.
    """
    def SquareArray(self, A):
        
        for i in range(len(A)):
            A[i] = A[i] * A[i]
        A.sort()
        
        return A
```
