# *Problem Statement :*

A company has `n` employees with a unique ID for each employee from `0` to `n - 1`. The head of the company has is the one with `headID`.

Each employee has one direct manager given in the `manager` array where `manager[i]` is the direct manager of the `i-th` employee, `manager[headID] = -1`. Also it's guaranteed that the subordination relationships have a tree structure.

The head of the company wants to inform all the employees of the company of an urgent piece of news. He will inform his direct subordinates and they will inform their subordinates and so on until all employees know about the urgent news.

The `i-th` employee needs `informTime[i]` minutes to inform all of his direct subordinates (i.e After informTime[i] minutes, all his direct subordinates can start spreading the news).

Return *the number of minutes* needed to inform all the employees about the urgent news.

## Sample Input

```cpp
Input: n = 1, headID = 0, manager = [-1], informTime = [0]
```

## Sample Output

```cpp
Output: 0
Explanation: The head of the company is the only employee in the company.
```

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a5d586ff-689c-4416-9bb2-87bd8ed3dcd2/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a5d586ff-689c-4416-9bb2-87bd8ed3dcd2/Untitled.png)

## Sample Input

```cpp
Input: n = 6, headID = 2, manager = [2,2,-1,2,2,2], informTime = [0,0,1,0,0,0]
```

## Sample Output

```cpp
Output: 1
Explanation: The head of the company with id = 2 is the direct manager of all the employees in the company and needs 1 minute to inform them all.
The tree structure of the employees in the company is shown.
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
class Solution(object):
    def numOfMinutes(self, n, headID, manager, informTime):
        
        def dfs(i):
            if manager[i] != -1:
                informTime[i] += dfs(manager[i])
                manager[i] = -1
            return informTime[i]
        
        return max(map(dfs,range(n)))
```

## Optimal Time Space Complexity :