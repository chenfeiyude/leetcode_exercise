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

# Solution 2. 0ms
1. If current value is bigger than previous sum + current value, no need to keep previous sum any more, so just reset current sum
to current value.

2. Keep the maximum current value.

```
class Solution {
    public int maxSubArray(int[] nums) {
        if(nums.length == 1)
            return nums[0];
        
        int r = nums[0];
        int currSum = r;
        for(int i = 1; i < nums.length; i++) {
            currSum += nums[i];
            
            if(currSum < nums[i]) 
                currSum = nums[i];// reset current sum to current value
            
            if(currSum > r) 
                r = currSum;
        }
        return r;
    }
}
```

# Solution 3. 1ms
Recursive way

```
class Solution {
    public int maxSubArray(int[] nums) {
        return maxSubArray(nums, nums[0], 1, nums[0]);
    }
    
    private int maxSubArray(int[] nums, int max, int currIndex, int currSum) {
        if(currIndex == nums.length)
            return max;
        
        int currValue = nums[currIndex];
        currSum += currValue;
        if(currSum < currValue)
            currSum = currValue;
        return maxSubArray(nums, currSum>max?currSum:max, currIndex+1, currSum);
    } 
}
```
