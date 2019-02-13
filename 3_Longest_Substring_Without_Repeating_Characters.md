# Problem

Given a string, find the length of the longest substring without repeating characters.

Example 1:

Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
Example 2:

Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
Example 3:

Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
             
             
# solution 1
brute force to find it!
1. for loop each char as start from the original string
2. if found diff, then exit the sub loop and get the length
3. keep the longest one

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int maxLength = 0;
        char[] charArray =  s.toCharArray();
        for(int i = 0; i < s.length(); i++) {
            int length = 1; // at least 1 length
            for(int j = i + 1; j < s.length(); j++) {
                String substr = s.substring(i, j);
                if(!substr.contains(charArray[j]+"")) {
                    length++;
                }
                else {
                    break;
                }
                   
            }
    
            if(length > maxLength )
                maxLength = length;
        }
        return maxLength;
    }
}
```

# solution 1 improvement 
1. do not call substring method every time
2. use set to store substring characters to check if any repeat incoming character

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int maxLength = 0;
        char[] charArray =  s.toCharArray();
        for(int i = 0; i < s.length(); i++) {
            Set<Character> subset = new HashSet<>();
            subset.add(charArray[i]);
            for(int j = i + 1; j < s.length(); j++) {
                if(subset.contains(charArray[j])) {
                    break;
                }
                subset.add(charArray[j]);
            }
    
            if(subset.size() > maxLength )
                maxLength = subset.size();
        }
        return maxLength;
    }
}
```
