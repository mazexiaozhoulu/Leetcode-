```
    def removeElement(self, A, elem):
        if not A or len(A) == 0:
            return 0
        start = 0
        end = len(A) - 1
        while start < end:
            while end >= 0 and A[end] == elem:
                end -= 1
            if start < end and A[start] == elem:
                A[start] = A[end]
                end -= 1
            start += 1
        return end + 1
```
