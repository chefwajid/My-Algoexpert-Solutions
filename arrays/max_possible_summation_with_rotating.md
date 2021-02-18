## Question:

Given an array, only rotation operation is allowed on array. We can rotate the array as many times as we want. Return the maximum possible summation of i*arr[i].

```
Input: arr[] = {1, 20, 2, 10}
Output: 72
We can get 72 by rotating array twice.
{2, 10, 1, 20}
20*3 + 1*2 + 10*1 + 2*0 = 72
```

```
Input: arr[] = {10, 1, 2, 3, 4, 5, 6, 7, 8, 9}
Output: 330
We can get 330 by rotating array 9 times.
{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
0*1 + 1*2 + 2*3 ... 9*10 = 330
```

[Find maximum value of Sum( i*arr[i]) with only rotations on given array allowed - GeeksforGeeks](https://www.geeksforgeeks.org/find-maximum-value-of-sum-iarri-with-only-rotations-on-given-array-allowed/)

```python
import time
## basically we just rotating the array to the right one by one element and checking which sum is great
def rotateOneElement(nums):
	n = len(nums) - 1
	temp = nums[0]
	nums[0] = nums[n]
	
	j = n
	
	while j >= 2:
		nums[j] = nums[j - 1]
		j -= 1
	
	nums[j] = temp
	
	sum_ = 0
	
	for i in range(len(nums)):
	    sum_ += nums[i] * i
	
	return sum_

start = time.time()		

nums = [10, 1, 2, 3, 4, 5, 6, 7, 8, 9]
max_ = float("-inf")
for i in range(len(nums) - 1):
    sum_ = rotateOneElement(nums)
    max_ = max(max_, sum_)

print(max_)

print("Total time:", time.time() - start)
```

Time complexity of the algorithm is O(n) and space complexity is O(1)  