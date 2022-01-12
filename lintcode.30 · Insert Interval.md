时间复杂度：O(n)O(n)，其中 nn 是数组 \textit{intervals}intervals 的长度，即给定的区间个数。

空间复杂度：O(1)O(1)。除了存储返回答案的空间以外，我们只需要额外的常数空间即可。
```
class Solution:
    """
    @param intervals: Sorted interval list.
    @param newInterval: new interval.
    @return: A new interval list.
    """
    def insert(self, intervals, newInterval):
        # write your code here
        left = []
        right = []
        start = newInterval.start
        end = newInterval.end
        for interval in intervals:
            #独立左边
            if interval.end < newInterval.start:
                left.append(interval)
            #独立右边
            elif interval.start > newInterval.end:
                right.append(interval)
            #interval和newinterval有重叠的部分的话，就start取小的，end取大的
            else:
                start = min(interval.start, start)
                end = max(interval.end, end)
        #再把重叠出来新的interval 命为tmp
        tmp = Interval(start, end)
        #在合并起来
        return left + [tmp] + right
```
