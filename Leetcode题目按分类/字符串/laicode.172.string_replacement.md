https://app.laicode.io/app/problem/172

双指针
in-place替换

物理意义，开闭区间
```java

  /**
  s: a[s+1.....]the characters that have been processed and should be kept
  f : the character being processed

  */

public class Solution {
  public String replace(String input, String s, String t) {
    // Assumption: input, s, t is not null. s is not empty
    char[] arr = input.toCharArray();
    if (s.length() >= t.length()) {
      return replaceShorter(arr, s, t);
    } 
    return replaceLonger(arr, s, t);
  }
  
  private String replaceShorter(char[] arr, String s, String t) {
    int slow = 0;
    int fast = 0;
    while (fast < arr.length) {
      if (fast <= arr.length - s.length() && equalString(arr, fast, s)) {
          copyString(arr, slow, t);
          fast += s.length();  //s is 原字符串
          slow += t.length();  //t is 目标字符串
      } else {
        arr[slow++] = arr[fast++];
      }
    }
    return new String(arr, 0, slow);   //[0...slow-1]是final solution
  }
  
  private String replaceLonger(char[] input, String s, String t) {
     // pre-compute
     List<Integer> matchIdx = getMatchEndIdx(input, s);
     char[] result = new char[input.length + matchIdx.size() * (t.length() - s.length())];
     int lastIndex = matchIdx.size() - 1;
     int slow = input.length - 1;
     int fast = result.length - 1;
     while (slow >= 0) {  //字符都填完了
       if (lastIndex >= 0 && slow == matchIdx.get(lastIndex)) {  
         copyString(result, fast - t.length() + 1, t);
         fast -= t.length();  
         slow -= s.length();
         lastIndex--;
       } else {
         result[fast--] = input[slow--];  // 要保留的字符
       }
     }
     return new String(result);
  }
  private void copyString(char[] arr, int index, String t) {
    for (int i = 0; i < t.length(); i++) {
      arr[index + i] = t.charAt(i);
    }
  }
  // start from index check s.length()个字符是否跟s match
  private boolean equalString(char[] arr, int index, String s) {
    for (int i = 0; i < s.length(); i++) {
      if (arr[i + index] != s.charAt(i)) {
        return false;
      }
    }
    return true;
  }
  private List<Integer> getAllMatches(char[] input, String s) {
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

}


```