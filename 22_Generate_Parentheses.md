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

# Solution 2. 20ms
recursive way 
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
            addResult(results, s, 1, n, n);
        }
        
        return results;
    }
    
    private void addResult(List<String> results, String current, int start, int end, int n) {
        // System.out.println(current + "," + start + "," + end);
        StringBuilder temp = new StringBuilder(current);
        if(temp.charAt(start) != temp.charAt(end)) {
            char ic = temp.charAt(start);
            temp.setCharAt(start, temp.charAt(end)); 
            temp.setCharAt(end, ic);
            if(!results.contains(temp.toString())
               && isMatchResult(temp.toString())) {
                results.add(temp.toString());
                addResult(results, temp.toString(), start, end, n);
            }
        }
        
        // no need to swap the last char
        if(end < n * 2 - 2)
            end++;
        else if(start < n - 1) {
            start++;
            end = n;
        }
        else
            return;
        
        addResult(results, current, start, end, n);
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
