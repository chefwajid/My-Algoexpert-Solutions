# *Solution 1 :*

## Explanation :

## Code :

```python
def selectionSort(array):
    
	for i in range(len(array)):
		k = i

		for j in range(i+1,len(array)):
			if array[j] < array[k]:
				k = j

		array[i] , array[k] = array[k] , array[i]
		
	return array
```

## Optimal Time Space Complexity :

**Best :** O ( N ) TIME | O ( 1 ) SPACE

**Average :** O ( N ^ 2 ) TIME | O ( 1 ) SPACE

**Worst :** O ( N ^ 2 ) TIME | O ( 1 ) SPACE