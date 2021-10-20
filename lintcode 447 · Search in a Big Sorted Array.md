先用倍增法 来确定 range。reader.get(range_len) 就是取数值，range_len就是下标
时间复杂度：O(logk)
空间复杂度 O(1)
```
class Solution:
    """
    @param reader: An instance of ArrayReader.
    @param target: An integer
    @return: An integer which is the first index of target.
    """
    def searchBigSortedArray(self, reader, target):
        # write your code here
        range_len = 1
        while reader.get(range_len-1) < target:
            range_len = range_len + range_len

        start, end = 0, range_len-1
        while start + 1 < end:
            mid = (start+end)//2
            if reader.get(mid) == target:
                end = mid
            elif reader.get(mid) < target:
                start = mid
            else:
                end = mid

        if reader.get(start) == target:
            return start
        if reader.get(end) == target:
            return end
        return -1
```
