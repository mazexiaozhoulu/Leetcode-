```
    def isIdentical(self, a, b):
        if not a and not b:
            return True
        elif not a or not b:
            return False
        
        if a.val != b.val:
            return False

        return self.isIdentical(a.left, b.left)and self.isIdentical(a.right, b.right)
```
