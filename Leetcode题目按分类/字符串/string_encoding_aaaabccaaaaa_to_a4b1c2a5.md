in-place


run-length encoding


aaaabccaaaaa
s
f
    f`

f`数到第一个不等于a的位置

a4aabccaaaaa
  s
    f
     f`
f挪到f`的位置， f`继续挪到第一个不等于b的位置

f` - f 等于1

每次f都是一段一段的跳


edge case:  abcde  +> a1b1c1d1e1
abcdexxxxxxx

step 1:只处理重复多次的字母
abcdex20

step 2: 专门处理那些单身的字母
abcdex20_ _ _ _ _
       f 
                s



```java
public class Solution {
  public String compress(String input) {
    // Write your solution here
    int slow = 0, fast = 0;
    char[] arr = input.toCharArray();
    int newLength  = 0;
    // step 1: deal with letters which occurence > 1
    while (fast < arr.length) {
      int begin = fast;
      while (fast < arr.length && arr[begin] == arr[fast]) {
        fast++;
      }
      //把字母拷贝过去
      arr[slow++] = arr[begin];
      if (fast - begin == 1) {
        newLength += 2;
      } else {
        // start from slow, copy digit equal to (fast-begin)
        int len = copyDigits(arr, slow, fast - begin);
        slow += len;
        newLength += len + 1;
      }
    }

   //  step 2:  deal with letter which occurence == 1
   char[] result = new char[newLength];
   // fast point to the letter being processed
   fast = slow - 1;
   // slow point to last index of new array
   slow = newLength - 1;
   while (fast >= 0) {
     // 碰到数字跳过
     if (Character.isDigit(arr[fast])) {
       while (fast >= 0 && Character.isDigit(arr[fast])) {
         result[slow--] = arr[fast--];
       }
     }else {
       result[slow--] = '1';
     }
     result[slow--] = arr[fast--];
   }
   return new String(result);
  }
  // count = 12;
  private int copyDigits(char[] input, int index, int count) {
    int len = 0;
    for (int i = count; i > 0; i /= 10) {
      index++;
      len++;
    }
    for (int i = count; i > 0; i /= 10) {
      int digit = i % 10;
      input[--index] = (char)('0' + digit);
    }
    return len;
  }
}

```