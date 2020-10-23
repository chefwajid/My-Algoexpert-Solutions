# *Problem Statement :*

**581. Shortest Unsorted Continuous Subarray**

LC **Easy**

Given an integer array, you need to find one **continuous subarray** that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order, too.

You need to find the **shortest** such subarray and output its length.

**Note:**

1. Then length of the input array is in range [1, 10,000].
2. The input array may contain duplicates, so ascending order here means **<=**.

**Example 1:**

```
Input: [2, 6, 4, 8, 10, 9, 15]
Output: 5
Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.

```

# *Solution 1 :*

## Explanation :

- First of all find all the unsorted elements in the Array

The Idea is that , among the unsorted elements , the SMALLEST UNSORTED ELEMENT's original index is the starting index for our problem.

- Similiarly for the largest unsorted element's orginal index (in sorted array) is last index;
- Algorithm:
    - Once all unsorted Elements are found , in the same traversal keep track of min/max
    - From start , find position of smallest unsorted elem and push that into a vector
    - From end , find position of Largest unsorted elem and push that into a vector
    - If vector empty return appropriate place holder.

## Code :

```cpp
class Solution {
public:
    int findUnsortedSubarray(vector<int>& a) {
        if(a.size()==1){return 0;}
        int min = INT_MAX;
        int max = INT_MIN;
        vector<int> resultIndices;

        //Find the max and min unsorted element
        for(int i=0 ; i<a.size() ; i++)
        {
            //edge case where index i-1 is not available
            if(i == 0)
            {
                 if(a[i] > a[i+1])minOrMax(min,max,a,i);
                 continue;
            }

            //edge case where index i+1 is not available
            if(i == a.size()-1)
            {
                //cout<<"msdfasfsdfsadfasdfax"<<a[i]<<a[i-1]<<endl;
                if (a[i] < a[i-1]){minOrMax(min,max,a,i);}
                continue;
            }

            //If it is greater than next element || smaller than previous --> it is unsorted
            if(a[i] > a[i+1] || a[i] < a[i-1])
            {
                minOrMax(min,max,a,i);
            }

        }

        //finding min element position
        for(int i=0 ; i<a.size() ; i++)
        {
            if(a[i] > min)
            {
                resultIndices.push_back(i);
                break;
            }
        }

        //finding max element position
        for(int i=a.size()-1 ; i >= 0  ; i--)
        {
            if(a[i] < max)
            {
                resultIndices.push_back(i);
                break;
            }
        }
            vector<int> empty;
        
        return resultIndices.size()<2 ? 0 : resultIndices[1] - resultIndices[0] + 1;
    }
    
    void minOrMax(int &min , int &max , vector<int> a , int i)
    {
        if(a[i] < min){min = a[i];}
        if(a[i] > max){max = a[i];}
    }
};
```

## Optimal Time Space Complexity : O(n) time with O(1) space