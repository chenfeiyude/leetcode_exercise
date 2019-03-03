# Problem
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Note that an empty string is also considered valid.

Example 1:

Input: "()"
Output: true
Example 2:

Input: "()[]{}"
Output: true
Example 3:

Input: "(]"
Output: false
Example 4:

Input: "([)]"
Output: false
Example 5:

Input: "{[]}"
Output: true

# Solution 1. 5ms
1. define a map to find out the correspondence char
2. use a stack to push in chars and pop chars if the top one matched the correspondence char.
3. if stack is empty then it is true

```java
class Solution {
    private static Map<Character, Character> map = new HashMap<>();
    static {
        map.put(')', '(');
        map.put(']', '[');
        map.put('}', '{');
    }
    public boolean isValid(String s) {
        char[] chars = s.toCharArray();
        Stack stack = new Stack();
        for(char c : chars) {
            // System.out.println(stack.peek());
            if (!stack.isEmpty() && map.containsKey(c) && (char)stack.peek() == map.get(c))
                stack.pop();
            else
                stack.push(c);  
        }
        
        if(stack.isEmpty())
            return true;
        return false;
    }
}
```
