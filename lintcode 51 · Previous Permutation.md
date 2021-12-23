
找到顶峰值，和比他小的调换，再把后面的从大到小排列，注意reverse 和 reversed

这两个函数都是对list中元素反向排序：. list.reverse(). reversed(list).

与 [52题](https://github.com/mazexiaozhoulu/Leetcode-/blob/d02852aee882a2609ad679bdac1609d76510b1ab/lintcode.52%20%C2%B7%20Next%20Permutation.md)类似 
```
class Solution:
    """
    @param: nums: A list of integers
    @return: A list of integers that's previous permuation
    """
    def previousPermuation(self, nums):
        # write your code here
        # write your code here
        if len(nums)<=1:
            return nums
        #从右向左扫过，寻找一个递增序列
        for i in range(len(nums)-2,-1,-1):
            #找到谷底的值
            if nums[i]>nums[i+1]:
                print(nums[i],nums[i+1])
                for k in range(len(nums)-1,i,-1):
                    if nums[k]<nums[i]:
                        print(nums[k],nums[i])
                        nums[i],nums[k]=nums[k],nums[i]
                        nums[i+1:]=reversed(nums[i+1:])
                        break
                break
            else:
                if i==0:
                    nums.reverse()
        return nums
```
