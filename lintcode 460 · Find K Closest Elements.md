```
class Solution:
    """
    @param A: an integer array
    @param target: An integer
    @param k: An integer
    @return: an integer array
    """
    def kClosestNumbers(self, A, target, k):
        # 思路到实践 1:没有想到双指针来找更小值
        #          2:没有注意到left，right超过范围的case
        #           3:双指针的设定错误
        result = []
        target_index = self.find_target(A, target)
        print(target_index)
        left = target_index -1
        right = target_index

        for _ in range(k):
            if left < 0:
                result.append(A[right])
                # print(result)
                right += 1
            elif right == len(A):
                result.append(A[left])
                left -= 1
            else:
                if target - A[left] <= A[right] - target:
                    result.append(A[left])
                    left -= 1
                else:
                    result.append(A[right])
                    right += 1

        return result
                
            
    def find_target(self, A, target):
        start, end = 0, len(A)-1
        while start + 1 < end:
            mid = (start + end) // 2
            if A[mid] < target:
                start = mid
            else:
                end = mid
        # 错误2号：>= 不是=
        if A[start] >= target:
            return start
        if A[end] >= target:
            return end
        # 错误1 号：如果这个值超出范围，就返回len(A), 不是-1
        return len(A)
```
