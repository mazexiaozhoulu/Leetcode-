先把range扩展，避免out of range

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
