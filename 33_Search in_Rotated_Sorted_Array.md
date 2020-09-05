# Problem

Given an integer array nums sorted in ascending order, and an integer target.

Suppose that nums is rotated at some pivot unknown to you beforehand (i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]).

You should search for target in nums and if you found return its index, otherwise return -1.

 ```
 Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
 ```
 
 ```
 Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
 ```
 
 # Solution 1
 O(n)
 
 ```
 class Solution {
    public int search(int[] nums, int target) {
        for(int i = 0; i < nums.length; i++) {
            if(nums[i] == target)
                return i;
        }
        return -1;
    }
}
 ```

# Solution 2
Binary search, make sure one half is sorted and check 
```
class Solution {
    public int search(int[] nums, int target) {
        int l = 0, r = nums.length -1;
        
        return findResult(l, r, nums, target);
    }
    
    private int findResult(int l, int r, int[] nums, int target) {
        if(l <= r) {
            int m = (l+r) / 2;
            
            if(target == nums[m]) {
                return m;
            }
            else if (l == r)
                return -1;
            else if (nums[l] <= nums[m]) {
                // left part is sorted, then check if target is in left
                if(target < nums[m] && target >= nums[l])
                    return findResult(l, m - 1, nums, target);
                else 
                    return findResult(m+1, r, nums, target);
            }
            else {
                // right part is sorted, then check if target is in right
                if(target > nums[m] && target <= nums[r])
                    return findResult(m+1, r, nums, target);
                else
                    return findResult(l, m - 1, nums, target);
                    
            }
        }
        
        return -1;
    }
    
}
```
