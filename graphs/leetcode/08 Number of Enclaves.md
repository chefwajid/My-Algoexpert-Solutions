# *Problem Statement :*

Given a 2D array `A`, each cell is 0 (representing sea) or 1 (representing land)

A move consists of walking from one land square 4-directionally to another land square, or off the boundary of the grid.

Return the number of land squares in the grid for which we **cannot** walk off the boundary of the grid in any number of moves.

## Sample Input

```cpp
Input: [
					[0,0,0,0],
					[1,0,1,0],
					[0,1,1,0],
					[0,0,0,0]
			]
```

## Sample Output

```cpp
Output: 3
Explanation: 
There are three 1s that are enclosed by 0s, and one 1 that isn't enclosed because its on the boundary.
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
class Solution(object):
    def numEnclaves(self, board):
        if(len(board)<=0):
            return []
        
        rows,cols = len(board),len(board[0])
        visited = set()
        directions = ((1,0),(0,1),(-1,0),(0,-1))
        
        def traverse(i,j):
            
            if (i,j) in visited:
                return
            
            visited.add((i,j))
            
            for a,b in directions:
                
                next_i,next_j = i+a,j+b
                
                if 0<= next_i < rows and 0<= next_j < cols and board[i][j]==1:
                    
                    
                    
                    #add your code
                    if board[next_i][next_j] == 1:
                        traverse(next_i,next_j)
            board[i][j] = 0
       
        
        for i in range(rows):
            for j in range(cols):
                if((i==0 or j==0 or i==rows-1 or j==cols-1) and board[i][j] == 1):
                    traverse(i,j)
        count = 0
        for i in range(rows):
            for j in range(cols):
                if board[i][j] == 1:
                    count+=1
                    
        
        return count
```

## Optimal Time Space Complexity :