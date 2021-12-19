快速选择算法

先确定，指针左边小于右边的时候，左边的数字 确实小于k；反之亦然；
不然就调换
```
class Solution:
    """
    @param nums: The integer array you should partition
    @param k: An integer
    @return: The index after partition
    """

    def partitionArray(self, nums, k):
        # write your code here
        left, right = 0, len(nums)-1
        while left <= right:
            while left <= right and nums[left] < k:
                left += 1
            while left <= right and nums[right] >= k:
                right -= 1
            if left <= right and (nums[left] > k or nums[right] <= k):
                left += 1
                right -= 1
        return left
```
