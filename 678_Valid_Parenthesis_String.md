# Problem
Given a string containing only three types of characters: '(', ')' and '*', write a function to check whether this string is valid. We define the validity of a string by these rules:

Any left parenthesis '(' must have a corresponding right parenthesis ')'.  
Any right parenthesis ')' must have a corresponding left parenthesis '('.  
Left parenthesis '(' must go before the corresponding right parenthesis ')'.  
'*' could be treated as a single right parenthesis ')' or a single left parenthesis '(' or an empty string.  

An empty string is also valid.  
Example 1:  
Input: "()"  
Output: True  
Example 2:  
Input: "(*)"  
Output: True  
Example 3:  
Input: "(*))"  
Output: True  


# Solution 1
1. Trying to put ( and * into a queue, remove the first element from the queue when ) appear
2. After the first loop, the queue will only contain ( and *, then we need to get rid of all (
3. if no ( left then it is true. Otherwise, false
4. this solution works for the examples above but failed on 
"(*()"

```java
class Solution {
    public boolean checkValidString(String s) {
        char[] chars = s.toCharArray();
        
        boolean isValid = true;
        LinkedList<Character> myQ = new LinkedList<>();
        for(int i = 0; i < s.length(); i++) {
            char curr = chars[i];
            if(curr != ')')
                myQ.add(curr);
            else {
                if(myQ.size() == 0)
                    return false;

                myQ.removeFirst();
            }
        }
        
        int n = 0;
        while(myQ.size() > 0) {
            char first = myQ.removeFirst();
            if(first == '(')
                n++;
            else if (n > 0)
                n--;
        }
        
        return n == 0;
    }
}
```

# Solution 1 bug fix
Instead of removing first element, remove the last '(' to keep more '*'

```java
class Solution {
    public boolean checkValidString(String s) {
        char[] chars = s.toCharArray();
        
        LinkedList<Character> myQ = new LinkedList<>();
        for(int i = 0; i < s.length(); i++) {
            char curr = chars[i];
            if(curr != ')')
                myQ.add(curr);
            else {
                System.out.println(myQ);
                if(myQ.size() == 0)
                    return false;
                if(!myQ.removeLastOccurrence('(')) {
                     myQ.removeFirst();
                }
            }
        }
        
        int n = 0;
        while(myQ.size() > 0) {
            char first = myQ.removeFirst();
            if(first == '(')
                n++;
            else if (n > 0)
                n--;
        }
        
        return n == 0;
    }
}
```
