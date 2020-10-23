# Problem Statement:

Given two non-empty arrays of integers, 

write a function that determines whether the second array is a subsequence of the first one.

A subsequence of an array is a set of that aren't necessarily adjacent in the array but that are in the same order as they appearin the array. 

For instance, the numbers [1, 3, 4] form a subsequence of the array [1, 2, 3, 4] , and so do the numbers [2, 4] . Note that a single in an array and the array itself are both valid subsequences of the array.

## Sample Input

```
array = [5, 1, 22, 25, 6, -1, 8, 10]
sequence = [1, 6, -1, 10]
```

## Sample Output

```
true
```

# *Solution 1 :*

## Explanation :

## Code :

```
def isValidSubsequence(array, sequence):
    
	count=0
	i=0
	
	while i < len(array) and count < len(sequence):
		if array[i] == sequence[count]:
			count+=1
		i+=1
			
	return count == len(sequence)
```

## Time Space Complexity :

O ( N ) TIME | O ( 1 ) SPACE