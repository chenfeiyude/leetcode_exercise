# Problem
Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

Example 1:

Input: 121
Output: true
Example 2:

Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
Example 3:

Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.

# Solution 1 76ms
1. Any negative value failed straight away
2. get reverse number and compare with the original number, if they are the same, then it is true.

```
class Solution {
    public boolean isPalindrome(int x) {
        if(x < 0)
            return false;
        int reverse = 0;
        int tmp = x;
        while (tmp > 0) {
            reverse = reverse * 10 + (tmp % 10 );
            tmp = tmp / 10;
        }
        
        return reverse == x;
    }
}
```
