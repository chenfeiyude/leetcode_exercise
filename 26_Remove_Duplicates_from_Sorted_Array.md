# Problem

Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Example 1:

```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.   
```

Example 2:

```
Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```

# Solution 1. 1ms
1. record the curr number as the first element
2. for loop the array, and compare curr and nums[i]. Update curr to nums[i] if diff and count one. Also set nums[i] to position of count

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if(nums.length == 0)
            return 0;
        int n = 1;
        int curr = nums[0];
        for(int num : nums) {
            if(num != curr) {
                curr = num;
                nums[n] = curr;
                n++;
            }
        }
        return n;
    }
}
```
