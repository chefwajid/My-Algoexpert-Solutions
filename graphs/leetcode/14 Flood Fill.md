# *Problem Statement :*

An `image` is represented by a 2-D array of integers, each integer representing the pixel value of the image (from 0 to 65535).

Given a coordinate `(sr, sc)` representing the starting pixel (row and column) of the flood fill, and a pixel value `newColor`, "flood fill" the image.

To perform a "flood fill", consider the starting pixel, plus any pixels connected 4-directionally to the starting pixel of the same color as the starting pixel, plus any pixels connected 4-directionally to those pixels (also with the same color as the starting pixel), and so on. Replace the color of all of the aforementioned pixels with the newColor.

At the end, return the modified image.

## Sample Input

```cpp
Input: 
image = [[1,1,1],[1,1,0],[1,0,1]]
sr = 1, sc = 1, newColor = 2
```

## Sample Output

```cpp
Output: [[2,2,2],[2,2,0],[2,0,1]]
Explanation: 
From the center of the image (with position (sr, sc) = (1, 1)), all pixels connected 
by a path of the same color as the starting pixel are colored with the new color.
Note the bottom corner is not colored 2, because it is not 4-directionally connected
to the starting pixel.
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
class Solution(object):
    def floodFill(self, image, sr, sc, newColor):
        
        rows,col = len(image),len(image[0])
        color = image[sr][sc]
        image[sr][sc] = newColor
        visited = set()
        directions = ((-1,0),(0,1),(1,0),(0,-1)) # up right down left
        
        def Traverse(i,j):
            
            if (i,j) in visited:
                return
            
            print(image[i][j])
            visited.add((i,j))
            
            for direction in directions:
                next_i,next_j = i+direction[0] , j+direction[1] 
                
                if 0 <= next_i < rows and 0 <= next_j < col and color==image[next_i][next_j]:
                    image[next_i][next_j] = newColor
                    Traverse(next_i,next_j)
                    
        
        Traverse(sr,sc)
        return image
```

## Optimal Time Space Complexity :