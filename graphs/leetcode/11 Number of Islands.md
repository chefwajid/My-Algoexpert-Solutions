# *Problem Statement :*

Given an `m x n` 2d `grid` map of `'1'`s (land) and `'0'`s (water), return *the number of islands*.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

## Sample Input

```cpp
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]

```

## Sample Output

```cpp
Output: 1
```

## Sample Input

```cpp
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]

```

## Sample Output

```cpp
Output: 3
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
class Solution(object):
    def numIslands(self, grid):
				#edge case
        if len(grid) <= 0:
            return 0

        rows,cols = len(grid),len(grid[0])
        visited = set()
        directions = ((1,0),(-1,0),(0,1),(0,-1))
        
        def traverse(i,j):
            
            if (i,j) in visited:
                return
            
            visited.add((i,j))
            
            for a,b in directions:
                next_i,next_j = i+a , j+b
                
                if 0 <= next_i < rows and 0 <= next_j < cols and grid[next_i][next_j]=="1":
                    #add code
                    traverse(next_i,next_j)
            grid[i][j] = "0"
                    
        count = 0
        for i in range(rows):
            for j in range(cols):
                if grid[i][j] == "1":
                    traverse(i,j)
                    count+=1
        
        return count
```

## Optimal Time Space Complexity :