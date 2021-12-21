先用倍增法 来确定 range。reader.get(range_len) 就是取数值，range_len就是下标
时间复杂度：O(logk)
空间复杂度 O(1)
优化：start从range_len = range_len开始，但不影响时间复杂度
```
    def searchBigSortedArray(self, reader, target):
        # write your code here
        range_len = 1
        #因为数据很大，所以根据题目，需要利用reader.get得到数据。
        #所以我们先需要利用倍增法， 找到比target大的数据，再在这个范围里找target。时间复杂度 o(logK)
        while reader.get(range_len-1) < target:
            range_len = range_len + range_len

        start, end = 0, range_len-1
        while start + 1 < end:
            mid = (start+end)//2
            if reader.get(mid) < target:
                start = mid
            else:
                end = mid
        #先判断小的index，万一两个index的值都是value的话，要取小的一个
        if reader.get(start) == target:
            return start
        if reader.get(end) == target:
            return end
        return -1
```
