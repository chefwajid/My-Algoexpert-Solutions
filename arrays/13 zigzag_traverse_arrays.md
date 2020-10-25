# Problem Statement:

Zigzag traverse
Write a function that takes in an n x m two-dimensional array (that can be square-shape)
and returns a one-dimensional array of all the array's elements in zigzag order.

## Sample Input

```cpp
array = [
    [1,3,4,10],
    [2,5,9,11],
    [6,8,12,15],
    [7,13,14,16],
]
```

## Sample Output

```cpp
output = [ 1 , 2 , 3 , 4 , 5 , 6 , 8 , 9 , 10 , 11 , 12 , 13 , 14 , 15 , 16 ]
```

# *Solution 1 :*

- [x]  Done on my own

## Explanation :

I traced the pattern, for a few cases and improvised at every turn.
Idea is to have two directional vectors in very loop. One from **north to east** and the other, **east to north**

## Code :

```cpp
t = [
    [1,3,4,10],
    [2,5,9,11],
    [6,8,12,15],
    [7,13,14,16],
]

rows = len(t)      #                                                                 N
cols = len(t[0])   #                                                              W     E  
i=0                #                                                                 S      
j=0

print("rows : " + str(rows))
print('cols : ' + str(cols))
print('\n')

while(i < rows and j<cols and i>-1 and j>-1):

        # first come north to west (downwards)

        # here we need to increase rows count and decrease cols count

        while(i < rows and j > -1 and i>-1 and j<cols):
         
            print(str(t[i][j]) + " --> ",end='')
            i += 1
            j-=1

        # go to next element for zigzag

        if i < rows:
            j += 1
        else:
            # 2,0 --> 3,-1 so to normalize --> 2,1
            i -= 1
            j += 2

        # then go upwards from south to east 

        # here we need to decrease rows count and increase cols count

        while(j < cols and i > -1 and j>-1 and i<rows):
            # print("second")
            # print(i,j)
            if i==rows-1 and j==cols-1:
                print(str(t[i][j]) , end = '')
                break

            print(str(t[i][j]) + " --> " , end='')
            j += 1
            i-=1

        # go to next element
        if j < cols:
            i+=1
        else:
            # 1,2 --> 0,3 so to normalize --> 2,2
            j-=1
            i+=2

# OUTPUT = 1 --> 2 --> 3 --> 4 --> 5 --> 6 --> 7 --> 8 --> 9 --> 10 --> 11 --> 12 --> 13 --> 14 --> 15 --> 16
```

## Time Space Complexity :

O(n^2) Time and O(1) Space