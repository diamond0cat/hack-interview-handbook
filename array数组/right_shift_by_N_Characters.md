

```java
package com.laioffer.sun;

public class RightShiftByNCharacters {
    public String rightShift(String input, int n) {
        // Write your solution here
        // sanity check
        if (input == null || input.length() <= 1) {
            return input;
        }

        char[] arr = input.toCharArray();
        int shift = n % input.length();

        reverse(arr, 0, arr.length - 1);
        reverse(arr, 0, shift - 1);
        reverse(arr, shift, arr.length - 1);

        return new String(arr);
    }

    private void reverse(char[] arr, int start, int end) {
        while (start <end) {
            char tmp = arr[start];
            arr[start] = arr[end];
            arr[end] = tmp;
            start++;
            end--;
        }
    }
}

```