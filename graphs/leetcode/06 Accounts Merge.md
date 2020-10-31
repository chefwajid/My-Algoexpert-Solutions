# *Problem Statement :*

Given a list `accounts`, each element `accounts[i]` is a list of strings, where the first element `accounts[i][0]` is a name, and the rest of the elements are emails representing emails of the account.

Now, we would like to merge these accounts. Two accounts definitely belong to the same person if there is some email that is common to both accounts. 

Note that even if two accounts have the same name, they may belong to different people as people could have the same name. 

A person can have any number of accounts initially, but all of their accounts definitely have the same name.

After merging the accounts, return the accounts in the following format: the first element of each account is the name, and the rest of the elements are emails **in sorted order**.

The accounts themselves can be returned in any order.

## Sample Input

```cpp
Input: 
accounts = [["John", "johnsmith@mail.com", "john00@mail.com"], ["John", "johnnybravo@mail.com"], ["John", "johnsmith@mail.com", "john_newyork@mail.com"], ["Mary", "mary@mail.com"]]
```

## Sample Output

```cpp
Output: [["John", 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com'],  ["John", "johnnybravo@mail.com"], ["Mary", "mary@mail.com"]]

Explanation: 
The first and third John's are the same person as they have the common email "johnsmith@mail.com".
The second John and Mary are different people as none of their email addresses are used by other accounts.
We could return these lists in any order, for example the answer [['Mary', 'mary@mail.com'], ['John', 'johnnybravo@mail.com'], 
['John', 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com']] would still be accepted.
```

# *Solution 1 :*

## Explanation :

## Code :

```python
class Solution(object):
    def accountsMerge(self, accounts):
        
        def find(x):
            return x if ds[x] < 0 else find(ds[x])
            
        def union(i,j):
            i,j = find(i),find(j)
            
            if i!=j:
                # Making i the parent
                ds[i] += ds[j]
                ds[j] = i
                
        c,ds,emailToId,idToName = 0,[],{},{}        
                
        for account in accounts:
            for email in account[1:]:
                if email not in emailToId:
                    emailToId[email] = c
                    idToName[c] = account[0]
                    ds.append(-1)
                    c+=1
                    
                union(emailToId[account[1]],emailToId[email])
                
        res = {}        
        for email,id in emailToId.items():
            root = find(id)
            res[root] = res.get(root,[]) + [email]
        
        print(res)
        return [[idToName[id]] + sorted(emails) for id,emails in res.items()]
```

## Optimal Time Space Complexity :

Amortized O ( N ) TIME with Path Compression and O ( N ^ 2 ) TIME without

[Accounts Merge - LeetCode](https://leetcode.com/problems/accounts-merge/submissions/)