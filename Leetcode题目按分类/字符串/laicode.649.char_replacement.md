
这里假设没有这种overlap的情况：
![picture 3](https://i.loli.net/2021/09/09/kGgl2hIpcoCqeKW.png)  



```java
public class Solution {
  public String replace(String input, String source, String target) {
    // Write your solution here
    // TODO: corner case
    // 没有overlap的情况
    char[] array = input.toCharArray();
    if (source.length() >= target.length()) {
      return replaceShorter(array, source, target);
    } 
    return replaceLonger(array, source, target);
  }
  private String replaceShorter(char[] input, String source, String target) {
    // two pointers
    int slow = 0, fast = 0;
    while (fast < input.length) {
      // found match pattern in input string, then replace
      if (fast <= input.length - source.length() && equalSubstring(input, fast, source)) {
        copySubstring(input, slow, target);
        slow += target.length();
        fast += source.length();
      } else {
        input[slow++] = input[fast++];
      }
    }
    return new String(input, 0, slow);
  }

  private String replaceLonger(char[] input, String source, String target) {
    ArrayList<Integer> matches = getAllMatches(input, source);
    // calculate the length of appending length
    char[] result = new char[input.length + matches.size() * (target.length() - source.length())];
    int lastIndex = matches.size() - 1;
    int fast = input.length - 1;
    int slow = result.length - 1;

    while (fast >= 0) {
      if (lastIndex >= 0 && fast == matches.get(lastIndex)) {
        copySubstring(result, slow - target.length() + 1, target);
        slow -= target.length();
        fast -= source.length();
        lastIndex--;
      } else {
        result[slow--] = input[fast--];
      }
    }
    return new String(result);
  }
  private ArrayList<Integer> getAllMatches(char[] input, String s) {
    ArrayList<Integer> matches = new ArrayList<>();

    int i = 0;
    while (i <= input.length - s.length()) {
      if (equalSubstring(input, i, s)) {
        // 记录每一个Matcched的pattern的end index
        matches.add(i + s.length() - 1);
        i += s.length();
      } else {
        i++;
      }
    }
    return matches;
  }

  private void copySubstring(char[] result, int fromIndex, String t) {
    for (int i = 0; i < t.length(); i++) {
      result[fromIndex + i] = t.charAt(i);
    }
  }
  private boolean equalSubstring(char[] input, int fromIndex, String s) {
    for (int i = 0; i < s.length(); i++) {
      if (input[fromIndex + i] != s.charAt(i)) {
        return false;
      }
    }
    return true;
  }
}

```