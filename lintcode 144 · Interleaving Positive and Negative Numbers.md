先把正负数 partition 开，然后再相向双指针进行交换。


```
class Solution:
    """
    @param: A: An integer array.
    @return: nothing
    """
    def rerange(self, A):
        pos, neg = 0, 0
        for num in A:#统计正负数量 o(n)的时间长度
        #只是一个局部变量，类型是int，记录的是正数的个数。这个不算额外空间的
        #如果 pos存储的是正数数组，只有这种情况，才算额外空间
            if num > 0:
                pos += 1
            else:
                neg += 1
        
        self.partition(A, pos > neg) #正数多的话，应该从正数打头
        self.interleave(A, pos == neg)

    #数组长度为单数，正数多正数打头；负数多负数打头
    def partition(self, A, start_positive):
        flag = 1 if start_positive else -1 # 如果start_positive是 正数 则flag=1
        left, right = 0, len(A) - 1
        #两个while，确定需要开始调换的指针定位
        while left <= right:
            while left <= right and A[left] * flag > 0:#如果左边的值大于0，正数打头的话不用变，直接下一个
                left += 1
            while left <= right and A[right] * flag < 0:#如果右边的值小于0，右边的指针不变
                right -= 1
            if left <= right: #如果正数多，还是负数打头的话，就调换
                A[left], A[right] = A[right], A[left]
                left += 1
                right -= 1

    #我想的方案只解决了这一种情况，就是数组长度为偶数的情况。
    def interleave(self, A, has_same_length):
        left, right = 1, len(A) - 1
        if has_same_length:
            right = len(A) - 2
            
        while left < right:
            A[left], A[right] = A[right], A[left]
            left, right = left + 2, right - 2
```
