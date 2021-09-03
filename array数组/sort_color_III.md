
使用分治法来解决。
传入两个区间，一个是颜色区间 color_from, color_to。另外一个是待排序的数组区间 index_from, index_to.
找到颜色区间的中点，将数组范围内进行 partition，<= color 的去左边，>color 的去右边。
然后继续递归。
时间复杂度 O(nlogk) n是数的个数， k 是颜色数目。这是基于比较的算法的最优时间复杂度。

不基于比较的话，可以用计数排序（Counting Sort）


```java
public class Solution {
  public int[] rainbowSortIII(int[] array, int k) {
    if (array == null || array.length == 0) return array;
    rainbowSort(array, 0, array.length - 1, 1, k);
    return array;
  }
  private void rainbowSort(int[] array, int left, int right, int minColor, int maxColor) {
    if (left >= right) return;
    if (minColor == maxColor) return;

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