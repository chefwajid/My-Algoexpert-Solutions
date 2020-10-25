# *Solution  :*

## Explanation :

Since minimum integer heap always returns the minimum element of all.

Insert whole array into the heap

## Code :

```python
def heapSort(array):
	result = []
    heap = MinIntHeap(len(array))
	heap.addList(array)
	while heap.peek() is not None:
		result.append(heap.poll())
	return result

class MinIntHeap:
	# you can find this class and many other in DSA / Templates folder
		

```

## Time Space Complexity :

**Best , Average and Worst :** O ( N * LOG(N) ) TIME | O ( 1 ) SPACE