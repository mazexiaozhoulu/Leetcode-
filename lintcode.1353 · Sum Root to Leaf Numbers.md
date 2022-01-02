Solution: Recursion
Time complexity: O(n)
Space complexity: O(h)
```
    def sumNumbers(self, root):
        # write your code here
        return self.dfs(root, 0);
    def dfs(self, root, prev):
        if(root == None) :
            return 0;

        sum = root.val + prev * 10;
        if(root.left == None and root.right == None) :
            return sum;

        return self.dfs(root.left, sum) + self.dfs(root.right, sum);
```
