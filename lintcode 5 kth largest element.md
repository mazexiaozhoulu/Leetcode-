如果用快速排序，排一下序再找第k个元素。就会花费nlog的排序时间。所以用quick select的算法

类似问题：找medium （k= n/2）

思想利用快速排序，快速排序第一步就是做partition（花费o(n)时间。如果k在左边就只去左边找k，所以把nlogn的规模问题，通过partition就变成了o（n/2）的时间）

```
class Solution:
    """
    @param k: An integer
    @param nums: An array
    @return: the Kth largest element
    """
    def kthLargestElement(self, k, nums):
        # write your code here
        if (nums == null):
            return = -1
        return self.quickSelect(nums, k, 0, len(nums)-1)

    def quickSelect(self, nums, k, start, end):
        if start == end:
            return nums[start]
        left, right = start, end
        pivot = nums[int((left+right)/2)]

        while (left <= right):
            while (left <= right and nums[left] > pivot):#从大到小的找，所以>的话就进行下一步
                left += 1
            while (left <= right and nums[right] < pivot):
                right -= 1
            if left <= right:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1

        if k-1 <= right:#说明要找的数在右边
            return self.quickSelect(nums, k, start, right)
        elif k-1 >= left:#在左边
            return self.quickSelect(nums, k, left, end)
        else:
            return pivot

```
