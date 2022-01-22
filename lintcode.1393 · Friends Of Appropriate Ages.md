```
class Solution:
    """
    @param ages: 
    @return: nothing
    整理好发送请求的条件，两个for循环即可解决问题
    """
    def numFriendRequests(self, ages):
        def request(a, b):
            return not (b <= 0.5 * a + 7 or b > a or b > 100 and a < 100)
        c = collections.Counter(ages)
        return sum(request(a, b) * c[a] * (c[b] - (a == b)) for a in c for b in c)

```
