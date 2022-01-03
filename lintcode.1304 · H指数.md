```
    def hIndex(self, citations):
        # write your code here
        citations.sort()
        n = len(citations)
        for i in range(n):
            if citations[i] >= (n-i):
                return n-i
        return 0
```
