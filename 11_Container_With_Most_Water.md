# Problem
Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2.

The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

Example:

Input: [1,8,6,2,5,4,8,3,7]
Output: 49

# Solution 1. 178ms
1. brute force to find out the max result
2. for loop each digit, compare each position's digit with its self, and the result = min_digit * (length of two position)

```java
class Solution {
    public int maxArea(int[] height) {
        int result = 0;
        for(int i = 0; i < height.length; i++) {
            int curri = height[i];
            for(int j = 0; j < i; j++) {
                int min = curri <= height[j]? curri : height[j];
                int tempr = min * (i - j);
                if(tempr > result)
                    result = tempr;
            }
        }
        
        return result;
    }
}
```

# Solution 2. 4ms
1. if i <= j, then i++ else j--
2. result = min * (j-i)
3. keep the max result

e.g.
-->i [1,8,6,2,5,4,8,3,7] j<--
i----j----min--result
0----8----1----8
1----8----7----49
1----7----3----18
1----6----8----40
2----6----6----24
3----6----2----6
4----6----5----10
5----6----4----4

result = 49

```java
class Solution {
    public int maxArea(int[] height) {
        int result = 0;
        int i = 0;
        int j = height.length - 1;
        while(i != j) {
            int min = 0;
            int tempi = i;
            int tempj = j;
            if(height[i] <= height[j])
                min = height[i++];
            else
                min = height[j--];
            
            int tempr = min * (tempj-tempi);
            // System.out.println(tempi + "----" + tempj + "----" + min + "----" + tempr);
            if(tempr > result)
                result = tempr;
        }
        
        return result;
    }
}
```
