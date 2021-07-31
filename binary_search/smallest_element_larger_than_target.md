

```java
public class Solution {
  public int smallestElementLargerThanTarget(int[] array, int target) {
    // Write your solution here
    if (array == null || array.length == 0) {
      return -1;
    }
    int left = 0;
    int right = array.length - 1;

    while (left < right) {
      int mid = left + (right - left) / 2;
      if (array[mid] == target) {
       left = mid + 1;
      } else if (array[mid] < target) {
        left = mid + 1;
      } else {
        right = mid;
      }
    }
    // only left 1 element
    if (array[left] > target) {
      return left;
    }
    return -1;
  }
}

```