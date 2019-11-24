# Problem

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

# Solution 1.  45ms 
1. find all the sums, and keep the max sum. really slow.

```
class Solution {
    public int maxSubArray(int[] nums) {
        int r = nums[0];
        for(int i = 0; i < nums.length; i++) {
            int currSum = nums[i];
            
            if(currSum > r) {
                r = currSum;
            }
            for(int j = i+1; j < nums.length; j++) {
            
                currSum += nums[j];
                if(currSum > r) {
                    r = currSum;
                }
            }
        }
        return r;
    }
}
```
