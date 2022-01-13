```
from collections import defaultdict
class Solution:
    """
    @param matrix: a 2D array
    @return: return a list of integers
    """
    def findDiagonalOrder(self, mat):
        # write your code here
        R, C = len(mat), len(mat[0])
        diagonalDict = defaultdict(list)
		# key - diagonal elements have the same r + c value.
        for r in range(R):
            for c in range(C):
                diagonalDict[r+c].append(mat[r][c])
                print(diagonalDict)
        ans = []
        for i, value in enumerate(diagonalDict.values()):
            if i % 2 == 0:
                ans += value[::-1]
            else:
                ans += value
        return ans
```
