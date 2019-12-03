# Problem
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:
```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

# Solution 1. 41ms
1. Brute force and check all the possibilities, but it is too slow

```
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> results = new ArrayList<>();
        if(n <= 0)
            return results;
        String s = "";
        for(int i = 0; i < n; i++)
        {
            s = "(" + s + ")";
        }
        results.add(s);
        if(n >= 2) {
            for(int i = 1; i < n; i++) {
                for(int j = n; j < 2*n - 1; j++) {
                    List<String> tempr = new ArrayList<>();
                    for(String temps : results) {
                        StringBuilder temp = new StringBuilder(temps);
                        char ic = temp.charAt(i);
                        temp.setCharAt(i, temp.charAt(j)); 
                        temp.setCharAt(j, ic);
                        if(!results.contains(temp.toString()) 
                           && !tempr.contains(temp.toString())
                           && isMatchResult(temp.toString()))
                            tempr.add(temp.toString());
                    }
                    results.addAll(tempr);
                }
            }
        }
        
        return results;
    }
    
    private boolean isMatchResult(String s) {
        char[] chars = s.toCharArray();
        int result = 0;
        for(char c : chars) {
            if(c == '(')
                result++;
            else
                result--;
            if(result < 0)
                return false;
        }
        return true;
        
    }
}
```
