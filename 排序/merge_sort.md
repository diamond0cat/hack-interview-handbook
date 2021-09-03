


```java
public class Solution {
  public int[] mergeSort(int[] array) {
    // Write your solution here
    if (array == null ||array.length <= 1) return array;

    int[] helper = new int[array.length];
    mergeSort(array, helper, 0, array.length - 1);

    return array;
  }

  private void mergeSort(int[] array, int[] helper, int left, int right) {
    if (left >= right) return;

    int mid = left + (right - left) / 2;

    mergeSort(array, helper, left, mid);
    mergeSort(array, helper, mid +1, right);
    combine(array, helper, left, mid, right);
  }

  private void combine(int[] array, int[] helper, int left, int mid , int right){
    // copy all elements to helper
    for (int i = left; i <= right; i++) {
      helper[i] = array[i];

    }

    int rightIndex = mid +1;
    int leftIndex = left;
    while (leftIndex <= mid && rightIndex <= right) {
      if (helper[leftIndex] <= helper[rightIndex]) {
        array[left++] = helper[leftIndex];
        leftIndex++;
      } else {
        array[left++] = helper[rightIndex];
        rightIndex++;
      }
    }
    while (leftIndex <= mid) {
      array[left++] = helper[leftIndex++];
    }
  }
}

 
 ```