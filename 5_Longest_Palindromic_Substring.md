# Problem

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example 1:

Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.   

Example 2:

Input: "cbbd"
Output: "bb"


# Solution 1.   513ms
This solution is too slow!!!
1. find all sub string start with and end with the same char
2. check if the sub string length > r, and also is palindrome. If it is, then set r = substr

```
class Solution {
    public String longestPalindrome(String s) {
        String r = "";
        if(!s.isEmpty()) {
            if(s.length() == 1)
                return s;
            
            char[] chars = s.toCharArray();
            r = chars[0] + "";
            for(int i = 0; i < chars.length; i++) {
                char c = chars[i];
                int next = s.indexOf(c, i + 1);
                while(next > 0) {
                    String candidate = s.substring(i, next + 1);
                    if(candidate.length() > r.length() && isPalindromic(candidate)) {
                        r = candidate;
                    }
                        
                    //System.out.println(i + "----" + next + "----" + candidate);
                    next = s.indexOf(c, next + 1);
                }
            }
        }
        return r;
    }
    
    private boolean isPalindromic(String s) {
        char[] chars = s.toCharArray();
        int halfSize = chars.length / 2;
        for(int i = 0; i < halfSize; i++) {
            if(chars[i] != chars[chars.length - 1 - i])
                return false;
        }
        return true;
    }
}
```

# Solution 1 improvement
1. Try the longest candidate first
2. exit the loop early

```
class Solution {
    public String longestPalindrome(String s) {
        String r = "";
        if(!s.isEmpty()) {
            if(s.length() == 1)
                return s;
            
            char[] chars = s.toCharArray();
            r = chars[0] + "";
            for(int i = 0; i < chars.length; i++) {
                if(chars.length - i < r.length())
                    break;// no need to check any more
                
                char c = chars[i];
                int next = s.lastIndexOf(c);
                while(next > i) {
                    String candidate = s.substring(i, next + 1);
                    if(candidate.length() > r.length() && isPalindromic(candidate)) {
                        r = candidate;
                        break;
                    }
                        
                    // System.out.println(i + "----" + next + "----" + candidate);
                    next = s.lastIndexOf(c, next - 1);
                    // System.out.println(next);
                }
            }
        }
        return r;
    }
    
    private boolean isPalindromic(String s) {
        char[] chars = s.toCharArray();
        int halfSize = chars.length / 2;
        for(int i = 0; i < halfSize; i++) {
            if(chars[i] != chars[chars.length - 1 - i])
                return false;
        }
        return true;
    }
}
```
