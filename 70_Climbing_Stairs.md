# Problem

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

Example 1:
```
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

Example 2:

```
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

# Solution 1. time out
recursive find out all the possibilities. Results matched while testing, but time exceed when submit.

```
class Solution {
    private int r = 0;
    public int climbStairs(int n) {
        cal(1, 0, n);
        cal(2, 0, n);
        
        return r;
    }
    
    private void cal(int current, int currentSum, int sum) {
        currentSum += current;
        
        if(currentSum > sum) {
            return;
        }
        else if (currentSum == sum) {
            r++;
            return;
        }
        
        cal(1, currentSum, sum);
        cal(2, currentSum, sum);
    }
}
```
