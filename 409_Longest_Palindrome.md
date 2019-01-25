# Problem
Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

This is case sensitive, for example "Aa" is not considered a palindrome here.

Note:
Assume the length of given string will not exceed 1,010.

Example:

Input:
"abccccdd"

Output:
7

Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.


# solution 1:
1. Calculate the counts for each char
2. Sum all the oven char's count
3. plus the longest cordinal count.

```
class Solution {
    public int longestPalindrome(String s) {
        if(s == null)
            return 0;
        else if(s.length() <= 1)
            return s.length();
            
        int maxLength = 0;
        Map<Character, Integer> charMap = new HashMap<>();
        for(char currentChar : s.toCharArray()) {
            int count = 1;
            if(charMap.containsKey(currentChar) ) 
                count = charMap.get(currentChar) + 1;
            charMap.put(currentChar, count);
        }
        
        int maxCordinalLength = 0;
        for(int count : charMap.values()) {
            if(count % 2 == 0) {
                maxLength += count;
            }
            else if (count > maxCordinalLength)
                maxCordinalLength = count;
        }
        
        maxLength += maxCordinalLength;
        return maxLength;
    }
}
```

# solution 1 bug fix:

solution 1 failed on test case
"civilwartestingwhetherthatnaptionoranynartionsoconceivedandsodedicatedcanlongendureWeareqmetonagreatbattlefiemldoftzhatwarWehavecometodedicpateaportionofthatfieldasafinalrestingplaceforthosewhoheregavetheirlivesthatthatnationmightliveItisaltogetherfangandproperthatweshoulddothisButinalargersensewecannotdedicatewecannotconsecratewecannothallowthisgroundThebravelmenlivinganddeadwhostruggledherehaveconsecrateditfaraboveourpoorponwertoaddordetractTgheworldadswfilllittlenotlenorlongrememberwhatwesayherebutitcanneverforgetwhattheydidhereItisforusthelivingrathertobededicatedheretotheulnfinishedworkwhichtheywhofoughtherehavethusfarsonoblyadvancedItisratherforustobeherededicatedtothegreattdafskremainingbeforeusthatfromthesehonoreddeadwetakeincreaseddevotiontothatcauseforwhichtheygavethelastpfullmeasureofdevotionthatweherehighlyresolvethatthesedeadshallnothavediedinvainthatthisnationunsderGodshallhaveanewbirthoffreedomandthatgovernmentofthepeoplebythepeopleforthepeopleshallnotperishfromtheearth"

Issue:
1. Didn't understand the question fully, and ignored the other cordinal chars.
2. Should add in other cordinal char length - 1 (which will be even)

```
class Solution {
    public int longestPalindrome(String s) {
        if(s == null)
            return 0;
        else if(s.length() <= 1)
            return s.length();
            
        int maxLength = 0;
        Map<Character, Integer> charMap = new HashMap<>();
        for(char currentChar : s.toCharArray()) {
            int count = 1;
            if(charMap.containsKey(currentChar) ) 
                count = charMap.get(currentChar) + 1;
            charMap.put(currentChar, count);
        }
        
        boolean foundEven = false;
        for(int count : charMap.values()) {
            if(count % 2 == 0) {
                maxLength += count;
            }
            else {
                if(!foundEven) {
                    maxLength += 1;
                    foundEven = true;
                }
                   
                maxLength += count - 1;
            }
        }
        
        return maxLength;
    }
}
```
# solution 2:
1. Calculate how many cornial chars
2. S length - number of cornial chars + 1

```
class Solution {
    public int longestPalindrome(String s) {
        if(s == null || s.length() == 0)
            return 0;
        
        int maxLength = s.length();
            
        Set<Character> cordinalSet = new HashSet<>();
        for(char currentChar : s.toCharArray()) {
            if(cordinalSet.contains(currentChar)) 
                cordinalSet.remove(currentChar);
            else
                cordinalSet.add(currentChar);
        }
        
        if(cordinalSet.size() > 0)
            maxLength = maxLength - cordinalSet.size() + 1;
        
        return maxLength;
    }
}
```
