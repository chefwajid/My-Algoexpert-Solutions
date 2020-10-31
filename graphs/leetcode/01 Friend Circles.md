# *Problem Statement :*

**547. Friend Circles**

**Medium**

There are **N** students in a class. Some of them are friends, while some are not. 

Their friendship is transitive in nature. 

For example, if A is a **direct** friend of B, and B is a **direct** friend of C, then A is an **indirect** friend of C. And we defined a friend circle is a group of students who are direct or indirect friends.

Given a **N*N** matrix **M** representing the friend relationship between students in the class. 

If M[i][j] = 1, then the ith and jth students are **direct** friends with each other, otherwise not. 

And you have to output the total number of friend circles among all the students.

# Example 1

## Sample Input

```cpp
Input: 
[[1,1,0],
 [1,1,0],
 [0,0,1]]
```

## Sample Output

```cpp
Output: 2
Explanation:The 0th and 1st students are direct friends, so they are in a friend circle. 
The 2nd student himself is in a friend circle. So return 2.
```

# Example 2

## Sample Input

```cpp
Input: 
				[[1,1,0],
				 [1,1,1],
				 [0,1,1]]
```

## Sample Output

```cpp
Output: 1
Explanation:The 0th and 1st students are direct friends, the 1st and 2nd students are direct friends, 
so the 0th and 2nd students are indirect friends. All of them are in the same friend circle, so return 1.
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
class Solution {
    
    private int size;
    
    private int[] sz;
    private int[] id;
    
    private int numOfComponents;
    
    
    
    public void init(int size)
    {
        this.size = numOfComponents = size;
        sz = new int[size];
        id = new int[size];
        
        for(int i=0;i<size;i++){
            sz[i] = 1;
            id[i] = i;
        }

    }
    
    public int findCircleNum(int[][] M) {
        int SizeOfMatrix = M.length;
        if(SizeOfMatrix <= 0){return 0;}
        else if(SizeOfMatrix == 1){return 1;}
        init(SizeOfMatrix);
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        
        for(int i=0 ;i<SizeOfMatrix ; i++){
            
            for(int j=0 ;j<M[0].length;j++)
            {
                if(i==j){continue;}
                
                if(M[i][j] == 1 && (map.get(i) == null || map.get(i) != j) && (map.get(j) == null  || map.get(j) != i))
                {
                    map.put(i,j);
                    map.put(j,i);
                    System.out.println(i);
                    System.out.println(j);

                    unify(i,j);
                }
                
            }
            
        }
        
        return numOfComponents;
    }
    
    public  int find(int p){
        int root = p;
        
        while(root != id[root]){root = id[root];}
        
        //compress path
        while(p!=root)
        {
            int next = id[p];
            id[p] = root;
            p = next;
        }
        
        return root;
    }
    
    public boolean connected(int p,int q)
    {
        return find(p) == find(q);
    }
    
    public void unify(int p, int q)
    {
        if(connected(p,q)){return;}
        
        int root1 = find(p);
        int root2 = find(q);
        
        if(sz[root1] >= sz[root2]){
            sz[root1] += sz[root2];
            id[root2] = root1;
        }else{
            sz[root2] += sz[root1];            
            id[root1] = root2;
            
        }
        
        numOfComponents--;

    }
    
    
    
}
```

## Optimal Time Space Complexity :

Amortized ( N ) TIME | O ( N ) Space

Amortized due to path compression