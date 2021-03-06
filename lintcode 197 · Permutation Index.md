想法：先把所有的都排出来，然后放到heap里，再去找这个排列的位置 需要的时间复杂度是 o(n!) 
但不可行，数据太大的话就会无法计算
只能直接计算比 当前数字 小的数字个数

要知道排列元素的所有排列按字典序排序后该排列的编号，可以通过求出小于这个排列的排列组合的数量num，那么答案就是num+1。
我们从第1位开始向后依次考虑，以[4,3,2,1]为例：
第1位：可选取的元素(3,2,1)小于第1位的元素有3个。假如我们固定第1位小于4的情况，那么第一位有3种，后面3位的排列组合数有3!种，所以比较到第1位就小于该排列的排列组合数共有3*3!=18种。
第2位：固定第1位为4，那么可选取的元素(2,1)小于第2位的元素有2个。后面2位的排列组合数有2!种，所以比较到第2位才小于该排列的排列组合数共有2*2!=4种。
第三位：固定第2位为3，那么可选取的元素(1)小于第3位的元素有1个。后面1位的排列组合数有1!种，所以比较到第3位才小于该排列的排列组合数共有1*1!=1种。
第四位：没有选择余地。
所以答案为18+4+1+1=24
```
class Solution:
    """
    @param A: An array of integers
    @return: A long integer
    """
    def permutationIndex(self, A):
        # write your code here
        n = len(A)
        factorial = 1
        sum = 1
        # 求出剩余可选择元素中小于自身的元素个数
        for i in range(n - 1, -1, -1):
            smaller = 0
            for j in range(i + 1, n):
                if A[j] < A[i]:
                    smaller += 1
            sum += smaller * factorial
            factorial *= (n - i)
        return sum;
```
