先找到第一个谷底，然后再找到第一个比他小的数字，swap。之后再把谷底之后的数字sorted 和 sort

sort 是应用在list 上的方法，sorted 可以对所有可迭代的对象进行排序操作
```
    def nextPermutation(self, nums):
        # write your code here
        if len(nums)<=1:
            return nums
        #从右向左扫过，寻找一个递增序列
        for i in range(len(nums)-2,-1,-1):
            #找到谷底的值
            if nums[i]<nums[i+1]:
                for k in range(len(nums)-1,i,-1):
                    if nums[k]>nums[i]:
                        print(nums[k],nums[i])
                        nums[i],nums[k]=nums[k],nums[i]
                        nums[i+1:]=sorted(nums[i+1:])
                        break
                break
            else:
                if i==0:
                    nums.sort()
        return nums
```
