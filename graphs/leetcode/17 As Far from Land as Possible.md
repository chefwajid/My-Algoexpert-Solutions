# *Problem Statement :*

Given an N x N `grid` containing only values `0` and `1`, where `0` represents water and `1` represents land, find a water cell such that its distance to the nearest land cell is maximized and return the distance.

The distance used in this problem is the *Manhattan distance*: the distance between two cells `(x0, y0)` and `(x1, y1)` is `|x0 - x1| + |y0 - y1|`.

If no land or water exists in the grid, return `1`.


## Sample Input

```cpp
Input: [[1,0,1],[0,0,0],[1,0,1]]
```

## Sample Output

```cpp
Output: 2
Explanation: 
The cell (1, 1) is as far as possible from all the land with distance 2.
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
def maxDistance(self, grid):
        
        # number of rows
        rows = len(grid)
        
        # number of columns
        cols = len(grid[0])
        
        # direction vectors
        directions = ((0,1),(0,-1),(1,0),(-1,0))
        
        # queue for BFS
        queue = deque()
        
        # create a new matrix 
        res = [[-1 for _ in range(cols)] for _ in range(rows)]
        
        # visit each cell
        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == 1:
                    res[r][c] = 0
                    queue.append((r,c))
        maximum = 0
        while queue:
            
            x,y = queue.popleft()
            
            for dx,dy in directions:
                
                # calculate next coord
                xx , yy = x + dx , y + dy
                
                # ignore if out of grid or not '-1'
                if xx < 0 or xx == rows or yy < 0 or yy == cols or res[xx][yy]!=-1:
                    continue
                    
                # update cell based on current cell
                res[xx][yy] = res[x][y] + 1
                maximum = max(res[x][y] + 1,maximum)

                
                # add to queue
                queue.append((xx,yy))
                
        # result is the maximum element in the matrix
        # as each cell represents the distance from the nearest 1
        # result = max([max(elem) for elem in res]) 
        
        # in the case of result being 0, a path has not been found
        # print(maximum)
        return maximum if maximum!=0 else -1
```

## Optimal Time Space Complexity :

[As Far from Land as Possible - LeetCode](https://leetcode.com/problems/as-far-from-land-as-possible)