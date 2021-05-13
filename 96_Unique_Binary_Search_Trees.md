# Problem
Given an integer n, return the number of structurally unique BST's (binary search trees) which has exactly n nodes of unique values from 1 to n.

Example 1:


Input: n = 3
Output: 5
Example 2:

Input: n = 1
Output: 1

# Solution 
```
class Solution {
    public int numTrees(int n) {
        if(n == 1)
            return 1;
        // define array with n+1 as we need 0 index and n index as well    
        int[] resultArray = new int[n+1];
        resultArray[0] = resultArray[1] = 1;
        for(int i = 2; i <= n; i++) {
            resultArray[i] = 0;
            for(int j = 0; j < i; j++) {
                resultArray[i] += resultArray[j] * resultArray[i - j - 1];
            }
        }
        return resultArray[n];
    }
}
```
