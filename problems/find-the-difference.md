# Find The Difference - from [LeetCode](https://leetcode.com)
[View this problem on LeetCode](https://leetcode.com/problems/find-the-difference/)

 Given two strings s and t which consist of only lowercase letters.

String t is generated by random shuffling string s and then add one more letter at a random position.

Find the letter that was added in t.

Example:

Input:
s = "abcd"
t = "abcde"

Output:
e

Explanation:
'e' is the letter that was added.

## My Solution - Version I
```java
class Solution {
    public char findTheDifference(String s, String t) {
        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        
        for (int i = 0; i < s.length(); i++){
            if (!map.containsKey(s.charAt(i))) map.put(s.charAt(i), 1);
            else map.put(s.charAt(i), map.get(s.charAt(i))+1);
        }
        
        for (int i = 0; i < t.length(); i++){
            if (map.containsKey(t.charAt(i))) map.put(t.charAt(i), map.get(t.charAt(i))-1);
        }
        
        for (Character key : map.keySet()){
            if (map.get(key) != 0) return key;
        }
        // error case
        return t.charAt(t.length()-1);
    }
}
```
## My Solution - Version II
```java
class Solution {
    public char findTheDifference(String s, String t) {
        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        
        for (int i = 0; i < s.length(); i++){
            if (!map.containsKey(s.charAt(i))) map.put(s.charAt(i), 1);
            else map.put(s.charAt(i), map.get(s.charAt(i))+1);
        }
        
        for (int i = 0; i < t.length(); i++){
            if (!map.containsKey(t.charAt(i)) || map.get(t.charAt(i))-1 < 0) return t.charAt(i);
            else map.put(t.charAt(i), map.get(t.charAt(i))-1);
        }
        
        return t.charAt(t.length()-1);
    }
}
```
## My Solution - Version III
```java
class Solution {
    public char findTheDifference(String s, String t) {
        int charCode = (int)t.charAt(s.length());
        
        for (int i = 0; i < s.length(); i++){
            charCode -= s.charAt(i);
            charCode += t.charAt(i);
        }
        return (char) charCode;
    }
}
```