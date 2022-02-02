## Description
Suppose a sorted array in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

## Example
Example 1:

Input：[4, 5, 6, 7, 0, 1, 2]

Output：0

Explanation：

The minimum value in an array is 0.

Example 2:

Input：[2,1]

Output：1

Explanation：

The minimum value in an array is 1.

```
class Solution:
    """
    @param nums: a rotated sorted array
    @return: the minimum number in the array
    """
    def findMin(self, nums):
        # write your code here
        if not nums:
            return 0

        start, end = 0, len(nums)-1
        while start + 1 < end:
            mid = (start+end) //2
            if nums[mid] < nums[mid - 1]:
                return nums[mid]
            else:
                if nums[mid] > nums[end]:
                    start = mid
                else:
                    end = mid

        return min(nums[start], nums[end])
```
