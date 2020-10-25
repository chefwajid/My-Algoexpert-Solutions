# *Solution 1 :*

## Explanation :

Implement insertion sort algorithm

## Code :

```cpp
def insertionSort(array):
    
	for i in range(1,len(array)):
		elementToAdd = array[i]
		
		# after adding/considering ith element
		# make sure it is sorted in our logical 2nd array
		for j in reversed(range(1,i+1)):
			if array[j] < array[j-1]:
				array[j] , array[j-1] = array[j-1] , array[j]
				
				
	return array
```

## Optimal Time Space Complexity :

**Best :** O ( N ) TIME | O ( 1 ) SPACE

**Average :** O ( N ^ 2 ) TIME | O ( 1 ) SPACE

**Worst :** O ( N ^ 2 ) TIME | O ( 1 ) SPACE