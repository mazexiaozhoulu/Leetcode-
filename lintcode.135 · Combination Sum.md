# 算法流程
# 1: 由于题目候选数字的集合candidates可能包含重复数字，且返回的结果要求组合内数字非降序，
# 因此首先需对candidates进行升序排序并去重，得到新的数字集合candidatesNew；

# 2:对新的数字集合进行深度优先搜索，传入的参数包括：数字集合candidatesNew、当前的位置index、当前存入的组合current、距离目标值的差remainTarget、保存答案的列表result；
# 3: 当remainTarget=0即达到边界，将current添加到result，回溯；
# 4: 循环遍历index位置到数字集合的末尾，分别递归调用dfs；
# 5: 递归步进为：remainTarget - candidatesNew[i]；
# 6: 剪枝：当发现当前的数字加入已超过remainTarget可进行剪枝。

时间复杂度：O( n^{target/min} )
（拷贝过程视作O(1)O(1)),n为集合中数字个数，min为集合中最小的数字
每个位置可以取集合中的任意数字，最多有target/min个数字。

空间复杂度：O( n^{target/min} ) n为集合中数字个数，min为集合中最小的数字
对于用来保存答案的列表，最多有n^{target/min}n 
target/min
 种组合
```
    def combinationSum(self, candidates, target):
        results = []
        # 集合为空
        if len(candidates) == 0:
            return results
        # 利用set去重后排序
        candidatesNew = sorted(list(set(candidates)))
        # dfs
        self.dfs(candidatesNew, 0, [], target, results)
        return results

    def dfs(self, candidatesNew, index, current, remainTarget,  results):
        # 到达边界
        if remainTarget == 0:
            return results.append(list(current))
        # 递归的拆解：挑一个数放入current
        for i in range(index, len(candidatesNew)):
            # 剪枝
            if remainTarget < candidatesNew[i]:
                break

            current.append(candidatesNew[i])
            self.dfs(candidatesNew, i, current, remainTarget - candidatesNew[i], results)
            current.pop()

```
