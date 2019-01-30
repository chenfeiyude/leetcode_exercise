# Problem 
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

# Solution 1
1. calculate sub of tartet and each number
2. if sub found in hashmap then return current number index and value of sub in map
3. if not found, then put current number and index into map
4. repeat step 2, 3

```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < nums.length; i++) {
            int sub = target - nums[i];
            if(map.containsKey(sub))
            {
                int i2 = map.get(sub);
                return i > i2? new int[]{i2, i} : new int[]{i, i2};
            }
            map.put(nums[i], i);
        }
        
        return new int[]{};
    }
}
```
