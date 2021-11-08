

```java
public class Solution {
  public String remove(String input, String t) {
    // Write your solution here
    char[] charArr = input.toCharArray();
    // build a set
    Set<Character> mySet = new HashSet<Character>();
    for (int i = 0; i < t.length(); i++) {
      mySet.add(t.charAt(i));
    }
    int fast = 0, slow = 0;
    while (fast < charArr.length) {
      if (!mySet.contains(charArr[fast])) {
       charArr[slow++] = charArr[fast++]; 
      } else {
        fast++;
      }
    } 
    return new String(charArr, 0, slow);
  }
}

```