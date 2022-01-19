# description

Given a sorted integer array where the range of elements are in the inclusive range [lower, upper], return its missing ranges.

# sample
 
Input:

nums = [0, 1, 2, 3, 7], lower = 0 and upper = 7

Output:

["4->6"]

Explanation:

in range[0,7],the missing range include range[4,6]
# 时间复杂度
O（n）
# 方法
#step:
         #a: extend nums, add lower and upper in nums
         #b: set two points, determine whether h - l >= 2; we don't need to consider about h - 1 < 2,which would show in result
         #c: if h - l >= 2 and h - l == 2, result add l+1
         #d: if h - l > 2, result add 'l+1'+'->'+'h-1'
         # attention:
             #1: after extend list, the range should be form 1 to len(nums);l should be nums[i-1], h should be nums[i]


```
    def findMissingRanges(self, nums, lower, upper):
        result = []
        nums = [lower-1] + nums + [upper+1]
        print(nums)
        for i in range(1, len(nums)):
            l = nums[i-1]
            h = nums[i]
            if h - l >= 2:
                if h - l == 2:
                    result.append(str(l+1))
                else:
                    result.append(str(l+1)+"->"+str(h-1))
        return result
```
