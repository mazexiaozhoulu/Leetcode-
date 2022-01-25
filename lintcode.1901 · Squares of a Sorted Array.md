# Description
Given an array of integers A sorted in non-decreasing order, return an array of the squares of each number, also in sorted non-decreasing order.

# Example
Example 1

Input: 
[-4,-1,0,3,10]
Output: 
[0,1,9,16,100]

# 解法一：排序
算法： sort排序
解题思路
直接原地平方，然后进行排序

复杂度分析
时间复杂度：O(nlogn)
排序需要nlogn的时间复杂度,n为数组长度。

```
class Solution:
    """
    @param A: The array A.
    @return: The array of the squares.
    """
    def SquareArray(self, A):
        
        for i in range(len(A)):
            A[i] = A[i] * A[i]
        A.sort()
        
        return A
```

# 解法二：双指针
算法：双指针
解题思路
左指针从头开始，右指针从尾开始，若相遇则结束。

复杂度分析
时间复杂度：O(n)
只需要遍历一遍数组，n为数组长度。

空间复杂度：O(n)
需要新开一个数组，n为数组长度。

```
class Solution:
    """
    @param A: The array A.
    @return: The array of the squares.
    """
    def SquareArray(self, A):
        
        left, right = 0, len(A) - 1
        answer = [0] * len(A)
        
        while left <= right:
            left_num, right_num = A[left] ** 2, A[right] ** 2
            answer[right - left] = max(left_num, right_num)
            left, right = left + (left_num > right_num), right - (left_num <= right_num)
        
        return answer
```
