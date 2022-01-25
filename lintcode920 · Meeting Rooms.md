# Description
Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), determine if a person could attend all meetings.

# sample 
Input: intervals = [(0,30),(5,10),(15,20)]

Output: false

Explanation: 

(0,30), (5,10) and (0,30),(15,20) will conflict

# complexity 

Time complexity : O(n \log n)O(nlogn). The time complexity is dominated by sorting. Once the array has been sorted, only O(n)O(n) time is taken to go through the array and determine if there is any overlap.
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
