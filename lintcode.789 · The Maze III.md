```
DIRECTIONS = {
    'u' : (-1, 0),
    'd' : (1, 0),
    'l' : (0,-1),
    'r' : (0, 1)
}


class Solution:
    """
    @param maze: the maze
    @param ball: the ball position
    @param hole: the hole position
    @return: the lexicographically smallest way
    """
    def findShortestWay(self, maze, ball, hole):
        # write your code here
        from heapq import heappush, heappop

        hole = (hole[0], hole[1])
        queue = [(0, '',  ball[0], ball[1])]
        distance = {(ball[0], ball[1]) : (0, '')}

        while queue:
            dist, path, x, y = heappop(queue)
            for direction in DIRECTIONS:
                if path and path[-1] == direction:
                    continue
                new_x, new_y = self.kick_ball(x, y, hole, maze, direction)
                new_dist = abs(x - new_x) + abs(y - new_y)
                if (new_x, new_y) in distance and distance[(new_x, new_y)] <= (dist + new_dist, path + direction):
                    continue
                distance[(new_x, new_y)] = (dist + new_dist, path + direction)
                heappush(queue, (dist + new_dist, path + direction, new_x, new_y))

        if hole in distance:
            return distance[hole][1]

        return 'impossible'

    def kick_ball(self, x, y, hole, maze, direction):
        delta_x, delta_y = DIRECTIONS[direction]
        new_x, new_y = x, y
        while not self.is_wall(new_x, new_y, maze):
            new_x += delta_x
            new_y += delta_y
            if (new_x, new_y) == hole:
                return new_x, new_y
        return new_x - delta_x, new_y - delta_y

    def is_wall(self, x, y, maze):
        if x < 0 or x > len(maze) - 1 or y < 0 or y > len(maze[0]) - 1:
            return True
        return maze[x][y] == 1
```
