# Problem

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

Example
```
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

# Solution 1. 1ms
1. define a list to store strings for digits 2-9, so the index = digit - 2. e.g digit 2's string index is 0, and 3 is 1
2. convert input string to index array. e.g. 23 -> [0, 1]
3. start from the first digit and for loop each char
4. use recursive method to find out all the combinations and store into a global set
5. return the result set as a list

```java
class Solution {
    private static String[] letters = new String[] {"abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    private Set<String> resultSet = new HashSet<>();
    public List<String> letterCombinations(String digits) {
        if(digits == null || digits.equals(""))
            return new ArrayList<>();
        char[] chars = digits.toCharArray();
        int[] digitArray = new int[digits.length()];
        for(int i = 0; i < digits.length(); i++) {
            digitArray[i] = Character.getNumericValue(chars[i]) - 2;
        }
        int index = 0;
        String digitStr = letters[digitArray[index]];
        
        chars = digitStr.toCharArray();
        for(char c : chars) {
            combinedStr(c + "", index, digitArray);
        }
        return new ArrayList<>(resultSet);
    }
    
    private void combinedStr(String currStr, int currIndex, int[] digitArray) {
        currIndex++;
        
        if(currIndex == digitArray.length) {
            resultSet.add(currStr);
        }
        else if(currIndex < digitArray.length) {
            String digitStr = letters[digitArray[currIndex]];
            char[] chars = digitStr.toCharArray();
            for(char c : chars) {
                combinedStr(currStr + c, currIndex, digitArray);
            }
        }
            
        
    }
}
```

#Solution 1. simplify codes. 1ms
```java
class Solution {
    private static Map<Character, char[]> lettersMap = new HashMap<>();
    static {
        lettersMap.put('2', new char[]{'a','b','c'});
        lettersMap.put('3', new char[]{'d','e','f'});
        lettersMap.put('4', new char[]{'g','h','i'});
        lettersMap.put('5', new char[]{'j','k','l'});
        lettersMap.put('6', new char[]{'m','n','o'});
        lettersMap.put('7', new char[]{'p','q','r','s'});
        lettersMap.put('8', new char[]{'t','u','v'});
        lettersMap.put('9', new char[]{'w','x','y','z'});
    }
    
    private Set<String> resultSet = new HashSet<>();
    public List<String> letterCombinations(String digits) {
        if(digits == null || digits.equals(""))
            return new ArrayList<>();
        combinedStr("", -1, digits.toCharArray());
        return new ArrayList<>(resultSet);
    }
    
    private void combinedStr(String currStr, int currIndex, char[] digitChars) {
        currIndex++;
        
        if(currIndex == digitChars.length) {
            resultSet.add(currStr);
        }
        else if(currIndex < digitChars.length) {
            char[] chars = lettersMap.get(digitChars[currIndex]);
            for(char c : chars) {
                combinedStr(currStr + c, currIndex, digitChars);
            }
        }
    }
}
```
