```

class Solution:
    """
    @param intervals: an array of meeting time intervals
    @return: if a person could attend all meetings
    """
    def canAttendMeetings(self, intervals):
        # Write your code here
        # 按起点排序
        intervals = sorted(intervals, key=lambda x: x.start)
        # 要维护的最大end
        maxend = -1
        for i in intervals:
            if i.start < maxend:
                return False
            maxend = max(maxend, i.end)
        return True
```
