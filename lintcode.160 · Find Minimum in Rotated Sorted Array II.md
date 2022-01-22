```
class Solution:
    def findMin(self, nums: List[int]) -> int:    
        low, high = 0, len(nums) - 1
        while low < high:
            pivot = low + (high - low) // 2
            if nums[pivot] < nums[high]:
                high = pivot 
            elif nums[pivot] > nums[high]:
                low = pivot + 1
            else:
                high -= 1
        return nums[low]
复杂度分析

时间复杂度：平均时间复杂度为 O(\log n)O(logn)，其中 nn 是数组 \it numsnums 的长度。如果数组是随机生成的，那么数组中包含相同元素的概率很低，在二分查找的过程中，大部分情况都会忽略一半的区间。而在最坏情况下，如果数组中的元素完全相同，那么 \texttt{while}while 循环就需要执行 nn 次，每次忽略区间的右端点，时间复杂度为 O(n)O(n)。

空间复杂度：O(1)O(1)。
```
