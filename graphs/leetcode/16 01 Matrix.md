# *Problem Statement :*

Given a matrix consists of 0 and 1, find the distance of the nearest 0 for each cell.

The distance between two adjacent cells is 1.

## Sample Input

```cpp
Input:
[[0,0,0],
 [0,1,0],
 [0,0,0]]
```

## Sample Output

```cpp
[[0,0,0],
 [0,1,0],
 [0,0,0]]
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
def updateMatrix(self, grid):
        # number of rows
        rows = len(grid)
        
        # number of columns
        cols = len(grid[0])
        
        # to keep track of cells in bfs
        queue = deque()
        
        # direction vectors
        directions = ((0,1),(0,-1),(1,0),(-1,0),)
        
        
        res = [[-1 for _ in range(cols)] for _ in range(rows)]
        
        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == 0:
                    res[r][c] = 0
                    queue.append((r,c))
                    
        
        while queue:
            x,y = queue.popleft()
            
            for dx,dy in directions:
                xx,yy = x + dx , y + dy
                
                if not (xx < 0 or xx==rows or yy < 0 or yy==cols) and res[xx][yy]==-1:
                    
                    res[xx][yy] = res[x][y] + 1
                    queue.append((xx,yy))
        return res
```

## Optimal Time Space Complexity :