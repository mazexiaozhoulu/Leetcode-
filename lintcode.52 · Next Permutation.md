# Description

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such an arrangement is impossible, it must rearrange it to the lowest possible order (i.e., sorted in ascending order).

The replacement must be in place and use only constant extra memory.
# sample

Input: nums = [1,2,3]

Output: [1,3,2]

# 时间复杂度

Time complexity : O(n)

Space complexity : O(1)

#方法 
从右往左，先找到第一个递减值，然后再找到最小的一个比他大的数字，swap。之后再把谷底之后的数字sorted 和 sort

sort 是应用在list 上的方法，sorted 可以对所有可迭代的对象进行排序操作

steps:

        #a: find the first decrease number from end as i
        
        #b: find the smallest number which bigger than i as j, from end make sure this is small.
        
        #c: swap i&j
        
        #d: sort th numbers which behind the i
        
        #e: dealing with the whole increase list or whole same number list
        
        # attention: 
        
            #1:when we compare i& i+1, there will have a out of range condition, so when we set the range, wo need to start form len(nums)-2
            
            #2:after sorted,we finish this list and we break
            
            #3:sorted & sort的区别
                
Time complexity : O(n)O(n). In worst case, only two scans of the whole array are needed.

Space complexity : O(1)O(1). No extra space is used. In place replacements are done.


```
    def nextPermutation(self, nums):
        if len(nums)<=1:
            return nums
        #a
        for i in range(len(nums)-2,-1,-1):
            if nums[i]<nums[i+1]:
            #b
                for k in range(len(nums)-1,i,-1):
                    if nums[k]>nums[i]:
                    #c
                        nums[i],nums[k]=nums[k],nums[i]
                        #d
                        nums[i+1:]=sorted(nums[i+1:])
                        break
                break
            else:
                if i==0:
                    nums.sort()
        return nums
```
