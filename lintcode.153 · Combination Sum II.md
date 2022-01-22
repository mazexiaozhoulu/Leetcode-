和combination sum I 其实是一个题，而且还更简单一点，唯一的区别是dfs递归的时候+1, 跳过重复使用当前数字。
时间复杂度：O(2^n \times n)O(2 
n×n)，其中 nn 是数组candidates 的长度。
```
class Solution:
    """
    @param num: Given the candidate numbers
    @param target: Given the target number
    @return: All the combinations that sum to target
    """
    def combinationSum2(self, num, target):
        result = []
        num.sort()
        self.dfs(result, [], 0, num, target)
        return result
    
    def dfs(self, result, path, index, num, target):
        if target == 0:
            result.append(path[:])
            return
        for i in range(index, len(num)):
            if num[i] > target:
                break
            if i != index and num[i-1] == num[i]:
                continue
            path.append(num[i])
            self.dfs(result, path, i+1, num, target - num[i])
            path.pop()
```
