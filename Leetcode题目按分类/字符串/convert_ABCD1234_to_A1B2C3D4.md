need to do it in-place

观察input

ABCD1234
分成4个section:
AB CD 12 34
                    分段翻转都是
AB 12 CD 34

A1 B2 C3 D4

![picture 1](https://i.loli.net/2021/09/10/pmKc2ea35EFtd1D.png)  


![picture 2](https://i.loli.net/2021/09/10/HeSJKCxE81g2i5u.png)  
字母和数字一样多，而且字母必须在数字左边



```java

public class ShuffleString {
    public static void main(String[] args) {
        String s = "abcde12345";
        char[] arr = s.toCharArray();
        System.out.println(shuffle(arr));
    }

    private  static String shuffle(char[] arr) {
        convert(arr, 0, arr.length - 1);
        return new String(arr, 0, arr.length);
    }
    private static void convert(char[] a, int left, int right) {
        // base case
        if (right - left <= 1) return;  // right-left+1 <= 2

        int size = right - left +1;
        int mid = left + size / 2;
        int leftMid = left + size / 4;
        int rightMid = left + size * 3 / 4;

        reverse(a, leftMid, mid - 1);
        reverse(a, mid, rightMid - 1);
        reverse(a, leftMid, rightMid - 1);

        convert(a, left, left + 2 *(leftMid - left) - 1);
        convert(a, left + 2 *(leftMid - left), right);
    }
    private static void reverse(char[] a, int left, int right) {
        while (left <right) {
            char tmp = a[left];
            a[left] = a[right];
            a[right] = tmp;
            left++;
            right--;
        }
    }
}

```