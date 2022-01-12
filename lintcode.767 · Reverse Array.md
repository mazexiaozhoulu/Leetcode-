时间复杂度：O(N)O(N)，其中 NN 为字符数组的长度。一共执行了 N/2 次的交换。
```
class Solution:
    """
    @param nums: a integer array
    @return: nothing
    """
    def reverseArray(self, nums):
        # write your code here
        for i in range(len(nums)//2):
            nums[i],nums[len(nums)-1-i] = nums[len(nums)-1-i],nums[i]
        return nums
```
