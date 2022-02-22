## Example
Example 1:

Input: rooms = [[1],[2],[3],[]]
Output: true
Explanation:  
We start in room 0, and pick up key 1.
We then go to room 1, and pick up key 2.
We then go to room 2, and pick up key 3.
We then go to room 3.  Since we were able to go to every room, we return true.
Example 2:

Input: rooms = [[1,3],[3,0,1],[2],[0]]
Output: false
Explanation: We can't enter the room with number 2.
## bfs
```
class Solution:
    """
    @param rooms: a list of keys rooms[i]
    @return: can you enter every room
    """
    def canVisitAllRooms(self, rooms):
        from collections import deque
        queue = deque([0])
        visited = set([0])
        while queue:
            room_id = queue.popleft()
            for next_room_id in rooms[room_id]:
                if next_room_id in visited:
                    continue
                queue.append(next_room_id)
                visited.add(next_room_id)
        return len(visited) == len(rooms)
```
