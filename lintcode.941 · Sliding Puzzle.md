## Example
Example 1:

Given board = `[[1,2,3],[4,0,5]]`, return `1`.

Explanation: 
Swap the 0 and the 5 in one move.
Example 2：

Given board = `[[1,2,3],[5,4,0]]`, return `-1`.

Explanation: 
No number of moves will make the board solved.
```
class Solution:
    """
    @param board: the given board
    @return:  the least number of moves required so that the state of the board is solved
    """
    def slidingPuzzle(self, board):
        final_state = [[1, 2, 3], [4, 5, 0]]
        source = self.matrix_to_string(board)
        target = self.matrix_to_string(final_state)

        from collections import deque
        queue = deque([source])
        distance = {source: 0}
        
        while queue:
            curr = queue.popleft()
            if curr == target:
                return distance[curr]
            for next in self.get_next(curr):
                if next in distance:
                    continue
                queue.append(next)
                distance[next] = distance[curr] + 1
        
        return -1

    def get_next(self, state):
        states = []
        direction = ((0, 1), (1, 0), (-1, 0), (0, -1))
        
        zero_index = state.find('0')
        x, y = zero_index // 3, zero_index % 3
        
        for i in range(4):
            x_, y_ = x + direction[i][0], y + direction[i][1]
            if 0 <= x_ < 2 and 0 <= y_ < 3:
                next_state = list(state)
                next_state[x * 3 + y] = next_state[x_ * 3 + y_]
                next_state[x_ * 3 + y_] = '0'
                states.append("".join(next_state))
        return states
        
    def matrix_to_string(self, state):
        str_list = []
        for i in range(2):
            for j in range(3):
                str_list.append(str(state[i][j]))
        return "".join(str_list)
```
