# Problem
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

Example 1:

Input: ["flower","flow","flight"]
Output: "fl"
Example 2:

Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.   

# Solution 1. 4ms
1. get the min length str
2. for loop each char in minstr and check if others are the same. If so then append to result.

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        String r = "";
        if(strs.length == 0)
            return r;
        
        String minStr = strs[0];
        for(String str : strs) {
            if(str.length() < minStr.length())
                minStr = str;
        }
        
        for(int i = 0; i < minStr.length(); i++) {
            char c = minStr.charAt(i);
            boolean isCommon = true;
            for(String str : strs) {
                if(str.charAt(i) != c)
                    isCommon = false;
            }
            
            if(!isCommon)
                break;
            r += c;
        }
        return r;
    }
}
```
