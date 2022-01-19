# Description
Given a non-overlapping interval list which is sorted by start point.
Insert a new interval into it, make sure the list is still in order and non-overlapping (merge intervals if necessary).

# Example 1:

Input:

interval list = [(1,2), (5,9)]

new interval = (2, 5)

Output:

[(1,9)]
# 时间复杂度

时间复杂度：O(n)，其中 nn 是数组intervals 的长度，即给定的区间个数。

空间复杂度：O(1)。除了存储返回答案的空间以外，我们只需要额外的常数空间即可。

# 方法
    # 独立左边的放左边
    # 独立右边的放右边
    # 重复的用max&min取大小做新的interval
    # 合并起来
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
