# Problem

Implement atoi which converts a string to an integer.

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned.

Note:

Only the space character ' ' is considered as whitespace character.
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.
Example 1:

Input: "42"
Output: 42
Example 2:

Input: "   -42"
Output: -42
Explanation: The first non-whitespace character is '-', which is the minus sign.
             Then take as many numerical digits as possible, which gets 42.
Example 3:

Input: "4193 with words"
Output: 4193
Explanation: Conversion stops at digit '3' as the next character is not a numerical digit.
Example 4:

Input: "words and 987"
Output: 0
Explanation: The first non-whitespace character is 'w', which is not a numerical 
             digit or a +/- sign. Therefore no valid conversion could be performed.
Example 5:

Input: "-91283472332"
Output: -2147483648
Explanation: The number "-91283472332" is out of the range of a 32-bit signed integer.
             Thefore INT_MIN (−231) is returned.
             
             
# Solution 1. 20 ms
1. use long to store result 
2. trim the string and try to conver to long directly. If it is a number then check if it is overflow and return max or min value if so. Otherwise return int value
3. for loop all chars and get digits 

```java
class Solution {
    public int myAtoi(String str) {
        Long r = 0l;
        str = str.trim();
        //System.out.println(str);
        try {
            r = Long.valueOf(str);
            return getInt(r);
        }
        catch(Exception e) {
            // it is not interger
        }
        
        if(!str.isEmpty()) {
            char[] chars = str.toCharArray();
            char first = chars[0];
            //System.out.println(first);
            if(isNumber(first) || first == '-' || first == '+') {
                StringBuilder rStr = new StringBuilder();
                rStr.append(first);
                for(int i = 1; i < chars.length; i++) {
                    System.out.println(chars[i]);
                    if(i <= 11 && isNumber(chars[i]))
                        rStr.append(chars[i]);
                    else 
                        break;
                }
                
                try {
                    r = Long.valueOf(rStr.toString());
                    return getInt(r);
                }
                catch(Exception e) {
                    // it is not interger
                    return 0;
                }
            }
        }
       
        return r.intValue();
    }
    
    private boolean isNumber(char c) {
        return c <= '9' && c >= '0';
    }
    
    private int getInt(Long r) {
        if(r > Integer.MAX_VALUE)
            return Integer.MAX_VALUE;
        else if (r < Integer.MIN_VALUE)
            return Integer.MIN_VALUE;
        return r.intValue();
    }
}
```
