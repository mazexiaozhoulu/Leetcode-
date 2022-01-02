时间复杂度：O( n^{target/min} )
（拷贝过程视作O(1)O(1)),n为集合中数字个数，min为集合中最小的数字
每个位置可以取集合中的任意数字，最多有target/min个数字。

空间复杂度：O( n^{target/min} ) n为集合中数字个数，min为集合中最小的数字
对于用来保存答案的列表，最多有n^{target/min}n 
target/min
 种组合
```
class Solution:
    """
    @param candidates: A list of integers
    @param target: An integer
    @return: A list of lists of integers
    """
    def combinationSum(self, candidates, target):
        # write your code here
        # 重复组合
        res = []
        if len(candidates) == 0:
            return res
        candidates = sorted(list(set(candidates)))
        self.backtracking(candidates,target,0,[],res)
        return res

    def backtracking(self, candidates,target, start,combination,res):
        if target == 0:
            return res.append(list(combination))

        else:
            for i in range(start,len(candidates)):
                if target < candidates[i]:
                    break
                combination.append(candidates[i])
                self.backtracking(candidates, target - candidates[i], i, combination, res)
                combination.pop()
```
