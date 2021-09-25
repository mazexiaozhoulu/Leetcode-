
```
class Solution:
    """
    @param: A: an integer array
    @return: A tree node
    """
    def sortedArrayToBST(self, A):
        # write your code here
        if not A:
            return None

        m = len(A) // 2
        root = TreeNode(A[m])
        root.right = self.sortedArrayToBST(A[m+1:])
        root.left = self.sortedArrayToBST(A[:m])

        return root
```
