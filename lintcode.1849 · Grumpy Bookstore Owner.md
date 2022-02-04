## Description
There is a bookstore. On the next nn days, customer[i]customer[i]customers will arrive on the i-thi−th day and leave at the end of that day.

However, the bookstore owner's temper is sometimes good but sometimes bad. We use an array of grumpygrumpy to indicate his temper is good or bad every day. If grumpy[i] = 1grumpy[i]=1, it means that the owner's temper is very bad on the day of ii. If grumpy[i] = 0grumpy[i]=0, it means that the owner has a good temper on the first day.

If the owner of the bookstore has a bad temper one day, it will cause all customers who come on that day to give bad reviews to the bookstore. But if one day you have a good temper, then all customers will give the bookstore favorable comments on that day.

The boss wanted to increase the number of people who gave favorable comments to the bookstore as much as possible and came up with a way. He can keep a good temper for XX days in a row. But this method can only be used once.

So how many people in this bookstore can give favorable comments to the bookstore when they leave on this nn day?

##
Example

Example 1:

Input:
[1,0,1,2,1,1,7,5]

[0,1,0,1,0,1,0,1]

3

Output: 

16

Explanation: 

The bookstore owner keeps themselves not grumpy for the last 3 days. 

The maximum number of customers that can be satisfied = 1 + 1 + 1 + 1 + 7 + 5 = 16.

## 时间复杂度

设总天数为N。
```
class Solution:
    """
    @param customers: the number of customers
    @param grumpy: the owner's temper every day
    @param X: X days
    @return: calc the max satisfied customers
    """
    def maxSatisfied(self, customers, grumpy, X):
        # write your code here
        sum = 0
        sum_window = 0
        for i in range(len(customers)):
            if i < X:
                sum_window += customers[i]
            else:
                sum_window += customers[i] * (1-grumpy[i])
        result = sum_window
        left, right = 0, X
        while right < len(customers):
            if grumpy[right] == 1:
                sum_window += customers[right]
            if grumpy[left] == 1:
                sum_window -= customers[left]

            result = max(sum_window,result)
            left += 1
            right += 1
        return result
```
