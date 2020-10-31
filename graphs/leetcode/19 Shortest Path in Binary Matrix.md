# *Problem Statement :*

In an N by N square grid, each cell is either empty (0) or blocked (1).

A *clear path from top-left to bottom-right* has length `k` if and only if it is composed of cells `C_1, C_2, ..., C_k` such that:

- Adjacent cells `C_i` and `C_{i+1}` are connected 8-directionally (ie., they are different and share an edge or corner)
- `C_1` is at location `(0, 0)` (ie. has value `grid[0][0]`)
- `C_k` is at location `(N-1, N-1)` (ie. has value `grid[N-1][N-1]`)
- If `C_i` is located at `(r, c)`, then `grid[r][c]` is empty (ie. `grid[r][c] == 0`).
- 

Return the length of the shortest such clear path from top-left to bottom-right. If such a path does not exist, return -1.

## Sample Input

```cpp
Input: [[0,0,0],[1,1,0],[1,1,0]]
```


## Sample Output

```cpp
Output: 4
```


# *Solution 1 :*

## Explanation :

[Breadth First Search Algorithm | Shortest Path | Graph Theory](https://www.youtube.com/watch?v=oDqjPvD54Ss)

## Code :

```cpp
class Solution(object):
    def shortestPathBinaryMatrix(self, grid):
        
        # number of rows
        rows = len(grid)
        
        # number of columns
        cols = len(grid[0])
        
        # direction vectors
        directions = ((0,1),(0,-1),(1,0),(-1,0),(1,1),(-1,-1),(-1,1),(1,-1),)
        
        # starting coord
        starting = (0,0)
        if grid[0][0] != 0: #if starting point not zero
            return -1
        
        # ending coord
        end = (rows-1,cols-1)
        
        #edge case with only one cell
        if starting == end:
            return 1 if grid[0][0]==0 else -1
        
        # keep track of previous nodes
        prev = {}
        
        # keep track of cells for BFS
        queue = deque([starting])
        
        # while there are cells in the queue keep looping
        while queue:
            x , y = queue.popleft()
            
            for dx,dy in directions:
                
                #calculate coords of next cell
                xx , yy = x + dx , y + dy
                
                #ignore cell if out of grid
                if xx < 0 or xx==rows or yy < 0 or yy == cols:
                    continue
                    
                #ignore if cell value is not zero
                if grid[xx][yy]!=0:
                    continue
                    
                #add cell in queue
                queue.append((xx,yy))
                
                #update cell
                grid[xx][yy] = 1
                
                prev[(xx,yy)] = (x,y)
                
                
        at = end
        count = 0
        
        while at is not starting and count < rows*cols:
            at = prev.get(at)
            count+=1
            print(at)
            if at == (0,0) or at is None:
                break
                
        if at != (0,0):
            return -1
        return count+1
```

## Optimal Time Space Complexity :