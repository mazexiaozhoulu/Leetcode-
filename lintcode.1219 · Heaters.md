## Description
Winter is coming! Your first job during the contest is to design a standard heater with fixed warm radius to warm all the houses.

Now, you are given positions of houses and heaters on a horizontal line, find out minimum radius of heaters so that all houses could be covered by those heaters.

So, your input will be the positions of houses and heaters seperately, and your expected output will be the minimum radius standard of heaters.

## Example
Example 1:

Input: [1,2,3],[2]

Output: 1

Explanation: The only heater was placed in the position 2, and if we use the radius 1 standard, then all the houses can be warmed.

Example 2:

Input: [1,2,3,4],[1,4]

Output: 1

Explanation: The two heater was placed in the position 1 and 4. We need to use radius 1 standard, then all the houses can be warmed.

## 二分法：
o（nlogn）
```
class Solution:
    """
    @param houses: positions of houses
    @param heaters: positions of heaters
    @return: the minimum radius standard of heaters
    """
    def findRadius(self, houses, heaters):
        # Write your code here
        heaters.sort()
        heat_radius = 0
        for house in houses:
            raius = self.get_minimum_radius(house,heaters)
            heat_radius = max(heat_radius, raius)
        return heat_radius

    def get_minimum_radius(self, house, heaters):
        left, right = 0, len(heaters)-1
        while left +1 < right:
            mid = left + (right - left) // 2
            if heaters[mid] <= house:
                left = mid
            else:
                right = mid

        left_distance = abs(heaters[left] - house)
        right_distance = abs(heaters[right] - house)
        return min(left_distance, right_distance)
```

## 双指怎 
o（n）
```
class Solution:
    """
    @param houses: positions of houses
    @param heaters: positions of heaters
    @return: the minimum radius standard of heaters
    """
    def findRadius(self, houses, heaters):
        # Write your code here
        n = len(houses)
        m = len(heaters)
        if n == 0:
            return 0

        houses.sort()
        heaters.sort()

        ret = 0
        j = 0
        for i in range(n):
            while j < m and heaters[j] <= houses[i]:
                j += 1

            disL, disR = sys.maxsize, sys.maxsize

            if j > 0 and heaters[j - 1] <= houses[i]:
                disL = houses[i] - heaters[j - 1]

            if j < m:
                disR = heaters[j] - houses[i]

            ret = max(ret, min(disL, disR))

        return ret
```
