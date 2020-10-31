# *Problem Statement :*

Given an array equations of strings that represent relationships between variables, each string `equations[i]` has length `4` and takes one of two different forms: `"a==b"` or `"a!=b"`. Here, `a` and `b` are lowercase letters (not necessarily different) that represent one-letter variable names.

Return `true` if and only if it is possible to assign integers to variable names so as to satisfy all the given equations.

## Sample Input

```cpp
Input: ["a==b","b!=a"]
```

## Sample Output

```cpp
Output: true
Explanation: We could assign a = 1 and b = 1 to satisfy both equations.
```

## Sample Input

```cpp
Input: ["a==b","b!=c","c==a"]
```

## Sample Output

```cpp
Output: false
```

## Sample Input

```cpp
Input: ["a==b","b==c","a==c"]
```

## Sample Output

```cpp
Output: true
```

# *Solution 1 :*

## Explanation :

## Code :

```python
class Solution(object):
    def equationsPossible(self,equations):
    
        def find(x):
            return x if UF[x]==x else find(UF[x])

        UF = {a : a for a in string.ascii_lowercase}

        for a,b,_,d in equations:
            if b == "=":
                UF[find(a)] = find(d)

                
        return not any(b=="!" and find(a) == find(d) for a,b,_,d in equations)
```

## Optimal Time Space Complexity :

Amortized O ( N ) TIME with Path Compression and O ( N ^ 2 ) TIME without