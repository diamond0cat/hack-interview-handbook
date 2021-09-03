

```java
public class Solution {
  public int[] quickSort(int[] array) {
      // Write your solution here
      if (array == null ||array.length <= 1) return array;

      quickSort(array, 0, array.length - 1);
      return array;
    }
    private void quickSort(int[] array, int left, int right) {
      if (left >= right) return;
      int pivotIndex = partition(array, left, right); // i <= pivotIndex ==> valu <= pivot, 

      quickSort(array, left, pivotIndex - 1);
      quickSort(array, pivotIndex + 1, right);
    }
      //所有<pivot的数放在pivot左边，所有>= pivot的数放在Pivot右边
    private int partition(int[] array, int left, int right) {
      int randomIndex = pickRandom(left, right);
      int pivot = array[randomIndex];

      swap(array, randomIndex, right);

      int leftIndex = left;
      int rightIndex = right- 1;

      while (leftIndex <= rightIndex) {
         if (array[leftIndex] <= pivot) {
           leftIndex++;
         } else if (array[rightIndex] > pivot) {
           rightIndex--;
         } else {
           swap(array, leftIndex, rightIndex);
           leftIndex++;
           rightIndex--;
         }
      }
      swap(array, leftIndex, right);
      return leftIndex;
    }
    private int pickRandom(int left, int right) {  // 2.....5    4
      return  left + (int)(Math.random() * (right - left + 1));
    }
    private void swap(int[] arr, int a, int b) {
      int tmp  = arr[a];
      arr[a] = arr[b];
      arr[b] = tmp;
    }
  
}

```
