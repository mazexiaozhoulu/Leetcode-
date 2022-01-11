#         #step:
#         #a: extend nums, add lower and upper in nums
#         #b: set two points, determine whether h - l >= 2; we don't need to consider about h - 1 < 2,which would show in result
#         #c: if h - l >= 2 and h - l == 2, result add l+1
#         #d: if h - l > 2, result add 'l+1'+'->'+'h-1'
#         # attention:
#             #1: after extend list, the range should be form 1 to len(nums);l should be nums[i-1], h should be nums[i]
 
        result = []
        nums = [lower-1] + nums + [upper+1]
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
