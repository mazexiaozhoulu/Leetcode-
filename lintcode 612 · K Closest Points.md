把所有的点放入最小堆，时间复杂度 O(NlogN)；空间复杂度O(N)
```
import heapq

class Solution:
    """
    @param points: a list of points
    @param origin: a point
    @param k: An integer
    @return: the k closest points
    """
    def kClosest(self, points, origin, k):
        # write your code here
        self.heap = []
        for point in points:
            dist = self.get_distance(point, origin)
            heapq.heappush(self.heap, (dist, point.x, point.y))
        
        result = []
        for _ in range(k):
            _, x, y = heapq.heappop(self.heap)
            result.append(Point(x, y))
        
        return result

    def get_distance(self, a, b):
        return (a.x - b.x)**2 + (a.y - b.y)**2
```
优化想法:利用最大堆（主要想法是，最小堆+取负）
```
from heapq import heappop, heappush


class Solution:
    """
    @param: points: a list of points
    @param: origin: a point
    @param: k: An integer
    @return: the k closest points
    """
    def kClosest(self, points, origin, k):
        if not points:
            return

        heap = []
        for point in points:
            distance = self.get_distance(origin, point)
            heappush(heap, (-distance, point))

            if len(heap) > k:
                heappop(heap)

        heap.sort(key=lambda item: (-item[0], item[1].x, item[1].y))

        return [p for _, p in heap]

    def get_distance(self, a, b):
        if not a or not b:
            return float('inf')

        a, b = (a.x - b.x), (a.y - b.y)

        return a * a + b * b
```
