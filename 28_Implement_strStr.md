# Problem
Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Example 1:

```
Input: haystack = "hello", needle = "ll"
Output: 2
```

Example 2:

```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

Clarification:

What should we return when needle is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when needle is an empty string. This is consistent to C's strstr() and Java's indexOf().

# Solution 1. 0ms
use java indexOf directly...did not understand the requirement fully

```
class Solution {
    public int strStr(String haystack, String needle) {
        if(needle == null || needle == "") {
            return 0;
        }
        
        int index = -1;
        if(haystack.contains(needle)) {
            index = haystack.indexOf(needle);    
        }
        
        return index;
    }
}
```

# Solution 2. 543 ms
brute force for loop all chars and compare

```java
class Solution {
    public int strStr(String haystack, String needle) {
        if(needle == null || needle.equals("")) {
            return 0;
        }
        
        int index = -1;
        for(int i = 0; i < haystack.length(); i++) {
            if(haystack.charAt(i) == needle.charAt(0)) {
                int length = 0;
                for(int j = 0; j < needle.length();) {
                    if(i + j >= haystack.length() || haystack.charAt(i + j) != needle.charAt(j)) {
                        break;
                    }
                    length = ++j;
                }
                
                if(length == needle.length()) 
                {
                    index = i;
                    break;
                }
            }
            
        }
        
        return index;
    }
}
```
