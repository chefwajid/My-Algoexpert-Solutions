# *Problem Statement :*

Given a non-empty 2D array `grid` of 0's and 1's, an **island** is a group of `1`'s (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

Find the maximum area of an island in the given 2D array. (If there is no island, the maximum area is 0.)

## Sample Input

```cpp
[
	 [0,0,1,0,0,0,0,1,0,0,0,0,0],
	 [0,0,0,0,0,0,0,1,1,1,0,0,0],
	 [0,1,1,0,1,0,0,0,0,0,0,0,0],
	 [0,1,0,0,1,1,0,0,1,0,1,0,0],
	 [0,1,0,0,1,1,0,0,1,1,1,0,0],
	 [0,0,0,0,0,0,0,0,0,0,1,0,0],
	 [0,0,0,0,0,0,0,1,1,1,0,0,0],
	 [0,0,0,0,0,0,0,1,1,0,0,0,0]
]
```

## Sample Output

```cpp
Given the above grid, return 6. 
Note the answer is not 11, 
because the island must be connected 4-directionally.
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
class Solution(object):
    def maxAreaOfIsland(self, board):
        # edge case
        if(len(board)<=0):
            return 0
        
        rows,cols = len(board),len(board[0])
        visited = set()
        directions = ((1,0),(0,1),(-1,0),(0,-1))
        count = 0
        nodes = {}
        
        def traverse(i,j):
            
            if (i,j) in visited:
                return
            
            visited.add((i,j))
            nodes[count]  = nodes.get(count,0) + 1
            
            for a,b in directions:
                
                next_i,next_j = i+a,j+b
                
                if 0<= next_i < rows and 0<= next_j < cols and board[next_i][next_j]==1:
                    
                    traverse(next_i,next_j)
                    
        
        for i in range(rows):
            for j in range(cols):
                if board[i][j]==1:
                    traverse(i,j)
                    count += 1
               
        area = [x for x in nodes.values()]  
        
        if(len(area)==0):
            return 0
        
        return max(area)
```

## Optimal Time Space Complexity :