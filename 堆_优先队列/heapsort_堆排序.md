

```java
public class Heapsort {
    public static void main(String[] args) {

    }
    public void heapSort(int[] arr) {
        // sanity check
        if (arr == null ||arr.length == 0) return;

        // step 1:heapify
        heapify(arr);
        // step 2: 每次都把最大的元素交换到最后的位置,做完以后arr里的元素从小到大排好
        for (int size = arr.length; size >1; size--) {  
            swap(arr, 0, arr.length - 1);  //每次都把最大的元素交换到最后的位置
            shiftDown(arr, 0, size - 1);
        }
    }
    private void heapify(int[] arr) {
        for (int i = arr.length / 2 - 1; i >= 0; i--) {  //这里index是从0开始的，所以最后一个非叶子节点是index2-1
            shiftDown(arr, i, arr.length);

        }
    }
    private void shiftDown(int[] arr, int index, int length) {

    }
}

```