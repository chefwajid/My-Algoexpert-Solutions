# *Solution  :*

## Explanation :

Quick Sort Implementation

## Code :

```python
def quickSort(array):
    
	partition(array,0,len(array)-1)
	return array

def partition(array,low,high):
	
	pivot = 0
	if low < high:
		
		pivot = quicksort(array,low,high)
		partition(array,low,pivot-1)
		partition(array,pivot+1,high)

def quicksort(arr, low, high):
    i = (low-1)         # index of smaller element
    pivot = arr[high]     # pivot
 	
	
	for j in range(low,high):
		
		if arr[j] <= pivot:
			i+=1
			arr[j] , arr[i] = arr[i] , arr[j]
			
	arr[i + 1] , arr[high] = arr[high] , arr[i+1]
	
	return i + 1
	
# The main function that implements QuickSort
# arr[] --> Array to be sorted,
# low  --> Starting index,
# high  --> Ending index
 
# Function to do Quick sort
```

## Time Space Complexity :

**Best :**         O ( N * LOG(N) ) TIME  |  O ( LOG(N) ) SPACE

**Average :**  O ( N * LOG(N) ) TIME  |  O ( LOG(N) ) SPACE

**Worst :**     O ( N ^ 2 ) TIME   |  O ( LOG(N) ) SPACE