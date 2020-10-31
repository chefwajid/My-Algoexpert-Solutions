# *Problem Statement :*

Given a 2D board containing `'X'` and `'O'` (**the letter O**), capture all regions surrounded by `'X'`.

A region is captured by flipping all `'O'`s into `'X'`s in that surrounded region.

## Sample Input

```cpp
Example:

X X X X
X O O X
X X O X
X O X X
```

## Sample Output

```cpp
After running your function, the board should be:

X X X X
X X X X
X X X X
X O X X

Explanation:

Surrounded regions shouldn’t be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. 
Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. 
Two cells are connected if they are adjacent cells connected horizontally or vertically.
```

# *Solution 1 :*

## Explanation :

Basically the O 's attached to border should be untouched, so what we do is, first do a DFS from the boundary O's and turn them to 1's, this ensures they are safe. Now change all O's to X , then all 1s to Os.

Reverse thinking of a question.

## Code :

```cpp
class Solution(object):
    def solve(self, board):
        # edge case
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
                
                if 0<= next_i < rows and 0<= next_j < cols and board[i][j]=="O":
                    
                    if board[next_i][next_j] == "O":
                        traverse(next_i,next_j)
                        
                        
            # change after For Loop to avoid repetition
            board[i][j] = 1
       
        
        for i in range(rows):
            for j in range(cols):
                # Start from boundary O's
                if((i==0 or j==0 or i==rows-1 or j==cols-1) and board[i][j] == "O"):
                    traverse(i,j)
        
        # change all 1's to O's and all O's to X                                                                      
        for i in range(rows):
            for j in range(cols):
                if board[i][j] == 1:
                    board[i][j]="O"
                elif board[i][j] == "O":
                    board[i][j] = "X"
                    
        
        return board
```

## Optimal Time Space Complexity :

O (  R * C ) Time and O ( R * C ) SPACE i guess

[Surrounded Regions - LeetCode](https://leetcode.com/problems/surrounded-regions/)