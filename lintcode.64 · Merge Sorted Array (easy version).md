```
    def mergeSortedArray(self, A, m, B, n):
        # write your code here
        if A is None and B is None:
            return 
        i, j = 0, 0
        array = []

        while i < m and j < n:
            if A[i] < B[j]:
                array.append(A[i])
                i += 1
            else:
                array.append(B[j])
                j += 1               
        while i < m:
            array.append(A[i])
            i += 1
        while j < n:
            array.append(B[j])
            j += 1

        for index in range(m + n):
            A[index] = array[index]

        return A


```
