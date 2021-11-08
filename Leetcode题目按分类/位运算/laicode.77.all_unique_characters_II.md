
acsii码一个int存不下，需要更多的int去存 ==>  bit vector

0-255一共256个字符

256 / 32= 8 一共需要8个integer


```java
Determine if the characters of a given string are all unique.

Assumptions

We are using ASCII charset, the value of valid characters are from 0 to 255
The given string is not null
Examples

all the characters in "abA+\8" are unique
"abA+\a88" contains duplicate characters
```



```java
public class Solution {
  public boolean allUnique(String word) {
    // Write your solution here
    char[] arr = word.toCharArray();
    int[] vec = new int[8]; // represent 256 character, from 0 to 255
    for (int i = 0; i < arr.length; i++) {
      if (((vec[arr[i] / 32] >>> (arr[i] % 32)) & 1) == 1) {    // /32是求第几行，%32是求第几列
          
        return false;
      }
      //把bit_vector[row]的第col位设为1
      vec[arr[i] / 32] |= 1 << (arr[i] % 32); 
    }
    return true;
  }
}

```
![picture 6](https://i.loli.net/2021/09/14/rTLf7tdRFqWBhHj.png)  

一维转二维


![picture 7](https://i.loli.net/2021/09/14/n7E2LImiwr1PqoY.png)  
