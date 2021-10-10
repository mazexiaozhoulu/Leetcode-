#merge sorted
```
    def mergeSortedArray(self, A, B):
        #two point
        if not A:
           return B
        if not B:
            return A
        la, lb = len(A),len(B)
        i, j = 0, 0
        res = []
         
        for k in range(la + lb):
            if i < la and (j >= lb or A[i] <= B[j]):
                res.append(A[i])
                i += 1
            else:
                res.append(B[j])
                j += 1

        return res
```
[leetcode 170](https://github.com/mazexiaozhoulu/Leetcode-/blob/7d1ea6f95340928f4c59cb64abae90cf55ebc4b3/leetcode%20179.%20Largest%20Number.md)

[75. Sort Colors](https://github.com/mazexiaozhoulu/Leetcode-/blob/fb046e55f525a1d529942c293eaff9d9940e4875/leetcode%2075.%20Sort%20Colors.md)
