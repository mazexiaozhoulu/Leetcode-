```
"""
Definition of Interval.
class Interval(object):
    def __init__(self, start, end):
        self.start = start
        self.end = end
"""

class Solution:
    """
    @param intervals: an array of meeting time intervals
    @return: the minimum number of conference rooms required
    """
    def minMeetingRooms(self, intervals):
        # Write your code here
        room=[]
        #加入开始时间和结束时间，1是房间+1，-1是房间-1
        for i in intervals:
            room.append((i.start,1))
            room.append((i.end,-1))
        tmp=0
        ans=0
        #排序
        room=sorted(room)
        #扫描一遍
        for idx,cost in room:
            tmp+=cost
            ans=max(ans,tmp)
        return ans
```
