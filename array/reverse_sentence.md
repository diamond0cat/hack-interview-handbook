
```java
package com.laioffer.sun;

import java.util.*;
public class ReverseSentence {
    public String reverseWords(String input) {
        // Write your solution here
        // two pointer

        // sanity check
        // I love Google
        if (input == null || input.length() <= 1) {
            return input;
        }

        char[] arr = input.toCharArray();
        reverse(arr, 0, arr.length - 1);
        int start = 0;
        for (int i = 0; i < input.length(); i++) {
            if (arr[i] != ' ' && (i == 0 || arr[i - 1] == ' ')) {
                start = i;
            }
            if (arr[i] != ' ' && ( i == arr.length - 1 || arr[i + 1] == ' ' )) {
                reverse(arr, start, i);
            }
        }
        return new String(arr);
    }
    private void reverse(char[] arr, int start, int end) {
        while (start < end) {
            char tmp = arr[start];
            arr[start] = arr[end];
            arr[end] = tmp;
            start++;
            end--;
        }
    }
}
```