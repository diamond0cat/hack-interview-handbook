
Given an array of balls, where the color of the balls can only be Red, Green, Blue or Black, sort the balls such that all balls with same color are grouped together and from left to right the order is Red->Green->Blue->Black. (Red is denoted by 0, Green is denoted by 1,  Blue is denoted by 2 and Black is denoted by 3).

Examples

{0} is sorted to {0}
{1, 0} is sorted to {0, 1}
{1, 3, 1, 2, 0} is sorted to {0, 1, 1, 2, 3}
Assumptions

The input array is not null.

```java
public class Solution {
  public int[] rainbowSortII(int[] array) {
           // Write your solution here
      if (array == null || array.length == 0) return array;
      rainbowSort(array, 0, array.length - 1, 0, 3);
      return array;
  }
  private void rainbowSort(int[] array, int left, int right, int minColor, int maxColor) {
    if (minColor == maxColor) return;
    if (left >= right) return;

    int midColor = (minColor + maxColor) / 2;
    int l = left, r = right;

    while (l <= r) {
      while (l <= r && array[l] <= midColor) {
        l++;
      }
      while (l <= r && array[r] > midColor) {
         r--;
      }
      if (l <= r) swap(array,  l++, r--);
    }
    rainbowSort(array, left, r, minColor, midColor);
    rainbowSort(array, l, right, midColor + 1, maxColor);
  }
  private void swap(int[] arr, int a, int b) {
    int tmp = arr[a];
    arr[a] = arr[b];
    arr[b] = tmp;
  }
}

```