# *Problem Statement :*

Sort using Bubble Sort Algorithm

## Sample Input

```cpp
array = [8, 5, 2, 9, 5, 6, 3]
```

## Sample Output

```cpp
[2, 3, 5, 5, 6, 8, 9]
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
def bubbleSort(array):
    
	for i in range(len(array)):
		for j in range(len(array)-i-1):
			
			if array[j] > array[j+1]:
				array[j] , array[j+1] = array[j+1] , array[j]  

	return array
```

## Optimal Time Space Complexity :

O ( N ^ 2 ) TIME | O ( 1 ) SPACE

Slowest sorting algorithm

**Best :** O ( N ) TIME | O ( 1 ) SPACE

**Average :** O ( N ^ 2 ) TIME | O ( 1 ) SPACE

**Worst :** O ( N ^ 2 ) TIME | O ( 1 ) SPACE


