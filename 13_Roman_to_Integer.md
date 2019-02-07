# Problem
1. define a map to find the related number for roman
2. for loop each digit of input int
    1). if next digit bigger than current digit, then use (next digit - current digit) as current sum. e.g. IV = 5 - 1 = 4
    2). if next digit equals to current digit, then (next digit - current digit) as current sum. e.g. III = 1 + 1 + 1 = 3
    3). if next digit smaller than current digit, then add current sum to total sum and set current sum to next digit

Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
For example, two is written as II in Roman numeral, just two one's added together. Twelve is written as, XII, which is simply X + II. The number twenty seven is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

I can be placed before V (5) and X (10) to make 4 and 9. 
X can be placed before L (50) and C (100) to make 40 and 90. 
C can be placed before D (500) and M (1000) to make 400 and 900.
Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.

Example 1:

Input: "III"
Output: 3
Example 2:

Input: "IV"
Output: 4
Example 3:

Input: "IX"
Output: 9
Example 4:

Input: "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
Example 5:

Input: "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.


# Solution 1

```
class Solution {
    private static Map<Character, Integer> sMap = new HashMap<>();
    {
        sMap.put('I', 1);
        sMap.put('V', 5);
        sMap.put('X', 10);
        sMap.put('L', 50);
        sMap.put('C', 100);
        sMap.put('D', 500);
        sMap.put('M', 1000);
    }
    public int romanToInt(String s) {
        char[] chars = s.toCharArray();
        int lastDigit = 0;
        int currentSum = 0;
        int sum = 0;
        for(char c : chars) {
            int curr = sMap.get(c);
            if(curr > lastDigit)
                currentSum = curr - lastDigit;
            else if(curr == lastDigit) 
                currentSum += lastDigit;
            else {
                sum += currentSum;
                currentSum = curr;
            }
            
            lastDigit = curr;
        }
        
        if(currentSum > 0)
            sum += currentSum;
        return sum;
    }
}
```
