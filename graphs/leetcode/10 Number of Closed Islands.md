# *Problem Statement :*

Given a 2D `grid` consists of `0s` (land) and `1s` (water). An *island* is a maximal 4-directionally connected group of `0s` and a *closed island* is an island **totally** (all left, top, right, bottom) surrounded by `1s.`

Return the number of *closed islands*.


## Sample Input

```cpp
Input: 
grid = 
				[
						[1,1,1,1,1,1,1,0],
						[1,0,0,0,0,1,1,0],
						[1,0,1,0,1,1,1,0],
						[1,0,0,0,0,1,0,1],
						[1,1,1,1,1,1,1,0]
				]
```

## Sample Output

```cpp
Output: 2
Explanation: 
Islands in gray are closed because they are completely surrounded by water (group of 1s).
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
def closedIsland(self, board):
        # edge case
        if(len(board)<=0):
            return []
        
        rows,cols = len(board),len(board[0])
        visited = set()
        directions = ((1,0),(0,1),(-1,0),(0,-1))
        count = 0
        nodes = {}
        corrupted = []
        
        def traverse(i,j):
            
            if (i,j) in visited:
                return
            
            visited.add((i,j))
            nodes[count]  = nodes.get(count,0) + 1
            
            for a,b in directions:
                
                next_i,next_j = i+a,j+b
                
                #once you touch a corner zero you're disqualified
                if board[next_i][next_j] == 5:
                    corrupted.append(count)
                    
                if 0<= next_i < rows and 0<= next_j < cols and board[next_i][next_j]==0:
                    
                    traverse(next_i,next_j)
                    
        for i in range(rows):
            for j in range(cols):
                #invalidate all corner zeroes so we know when we touch one
                if (i==0 or j==0 or i== rows-1 or j == cols-1) and board[i][j]==0:
                    board[i][j] = 5
        
        
        for i in range(rows):
            for j in range(cols):
                #Dont start from corners and only from 0's in between
                if (i!=0 and j!=0 and i!= rows-1 and j!= cols-1) and board[i][j]==0:
                    
                    traverse(i,j)
                    count += 1
                    
        
        output = 0
        for x,y in nodes.items():
            if x not in corrupted:
                output +=1
                
        return output
```

## Optimal Time Space Complexity :