# Problem

Given a 32-bit signed integer, reverse digits of an integer.

Example 1:

Input: 123
Output: 321
Example 2:

Input: -123
Output: -321
Example 3:

Input: 120
Output: 21
Note:
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

# Solution 1 58ms
1. put all the digits into a stack
2. pop all the digits from the stack, then it will be reverse
3. if the first digit of reverse number is not equals the last digit of the original number, then it is overflow

```java
class Solution {
    public int reverse(int x) {
        Stack<Integer> stack = new Stack<>();
        int flag = x < 0? -1 : 1;
        x = x * flag;
        int lastDigit = 0;
        while(x > 0) {
            //System.out.println(x);
            lastDigit = x % 10; 
            stack.push(lastDigit);
            x = x / 10;
        }
        
        int result = 0;
        int n = 1;
        while (!stack.isEmpty()) {
            lastDigit = stack.pop();
            result += lastDigit * n;
            // System.out.println(lastDigit + "---------" + result);
            if(!stack.isEmpty())
                n *= 10;
        }
        
        // System.out.println(result / n +"?" + n);
        if(n != 0 && result / n != lastDigit)
            return 0;//overflow
        
        return result * flag;
    }
}
```

# Solution 2  16ms
1. do the pop and push in one same loop
2. check the first digit of the reverse int if equals to the last digit of the input int. It will be changed if it is overflow
3. if the last digit of the input int is 0, it will never overfollow so we dont need to check that for this case

```java
class Solution {
    public int reverse(int x) {
        int flag = x < 0? -1 : 1;
        x = x * flag;
        int lastDigit = 0;
        int result = 0;
        int n = 1;
        int firstDigit = x % 10;
        int lastN = n;
        while(x > 0) {
            lastDigit = x % 10; 
            if(result == 0)
                result = lastDigit;
            else 
                result = result * 10 + lastDigit;
                
            x = x / 10;
            lastN = n;
            n = n * 10;
        }
        
        if(firstDigit > 0 && result / lastN != firstDigit)
            return 0;
        return result * flag;
    }
}
```
