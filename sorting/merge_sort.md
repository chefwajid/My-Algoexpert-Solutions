# *Solution  1:*

Apply Merge Sort

## Code :

```python
# Recursive Python Program for merge sort

def merge(left, right):
	if not len(left) or not len(right):
		return left or right

	result = []
	i, j = 0, 0
	while (len(result) < len(left) + len(right)):
		if left[i] < right[j]:
			result.append(left[i])
			i+= 1
		else:
			result.append(right[j])
			j+= 1
		if i == len(left) or j == len(right):
			result.extend(left[i:] or right[j:])
			break

	return result

def mergesort(list):
	if len(list) < 2:
		return list

	middle = len(list)/2
	left = mergesort(list[:middle])
	right = mergesort(list[middle:])

	return merge(left, right)
```

## Time Space Complexity :

**Best :**         O ( N * LOG(N) ) TIME  |  O ( 1 ) SPACE

**Average :**  O ( N * LOG(N) ) TIME  |  O ( 1 ) SPACE

**Worst :**     O ( N * LOG(N) ) TIME   |  O ( 1 ) SPACE