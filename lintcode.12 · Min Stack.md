```
class MinStack:
    
    def __init__(self):
        self.stack = []
        self.min_stack = []

    """
    @param: number: An integer
    @return: nothing
    """
    def push(self, number):
        self.stack.append(number)
        if not self.min_stack or number <= self.min_stack[-1]:
            self.min_stack.append(number)

    """
    @return: An integer
    """
    def pop(self):
        if self.stack:
            number = self.stack.pop()
            if number == self.min_stack[-1]:
                self.min_stack.pop()
            return number
        else:
            return None

    """
    @return: An integer
    """
    def min(self):
        if self.min_stack:
            return self.min_stack[-1]
```
