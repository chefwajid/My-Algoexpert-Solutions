# Problem Statement:

Move Element To End You're given an array of integers and an integer. 

Write a function that moves all instances of that integer in the array to the end of the array and returns the array. The function should perform this in place (i.e., it should mutate the input array) and doesnt need to maintain the order of the other integers.

## Sample Input

```cpp
array = [2, 1, 2, 2, 2, 3, 4, 2]
toMove = 2
```

## Sample Output

```cpp
[1, 3, 4, 2, 2, 2, 2, 2]
```

# *Solution 1 :*

- [x]  Done on my own

## Explanation :

## Code :

```cpp
def moveElementToEnd(array, toMove):
    
	count = 0
	
	for i in range(len(array)):
		
		if array[i] != toMove:
			array[count] = array[i]
			count+=1
			
	while count < len(array):
		array[count] = toMove
		count+=1
		
	return array
```

## Time Space Complexity :

O ( N ) TIME | O ( 1 ) SPACE