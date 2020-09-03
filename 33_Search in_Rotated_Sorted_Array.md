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
