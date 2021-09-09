https://app.laicode.io/app/problem/172

双指针
in-place替换

```java
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
          fast += s.length();
          slow += t.length();
      } else {
        arr[slow++] = arr[fast++];
      }
    }
    return new String(arr, 0, slow);
  }
  
  /**
  s: a[s+1.....]the characters that have been processed and should be kept
  f : the character being processed

  */
  private String replaceLonger(char[] input, String s, String t) {
     // pre-compute
     List<Integer> matchIdx = getMatchEndIdx(input, s);  //找出匹配的子串的总数
     char[] result = new char[input.length + matchIdx.size() * (t.length() - s.length())];  //分配多余的空间
     int lastIndex = matchIdx.size() - 1;  //index从后往前开始填字符
     int slow = input.length - 1;
     int fast = result.length - 1;
     while (slow >= 0) {
       if (lastIndex >= 0 && slow == matchIdx.get(lastIndex)) {
         copyString(result, fast - t.length() + 1, t);
         fast -= t.length();
         slow -= s.length();
         lastIndex--;
       } else {
         result[fast--] = input[slow--];
       }
     }
     return new String(result);
  }
  private void copyString(char[] arr, int index, String t) {
    for (int i = 0; i < t.length(); i++) {
      arr[index + i] = t.charAt(i);
    }
  }



  private List<Integer> getMatchEndIdx(char[] arr, String s) {
    List<Integer> result = new ArrayList<>();
    int i = 0;
    while (i <= arr.length - s.length()) {
      if (equalString(arr, i, s)) {
        result.add(i + s.length() - 1);
        i += s.length();
      } else {
        i++;
      }
    }
    return result;
  }
}

```