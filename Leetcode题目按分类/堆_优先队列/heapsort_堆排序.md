


```java
// time = O(nlogn)这是时间复杂度，不是运行时间  space = O(1) non-stable
//每一步都是logn的，repeat n次
public class Heapsort {
    public static void main(String[] args) {
        int[] test = new int[]{1, 5, -1, -9, 19};

        Heapsort hs = new Heapsort();
        hs.heapSort(test);

        for (int num :test) {
            System.out.print(num + " ");
        }
    }
    public void heapSort(int[] arr) {
        // sanity check
        if (arr == null ||arr.length == 0) return;

        // step 1:heapify
        heapify(arr);
        for (int num : arr) {
            System.out.print(num + " ");
        }
        System.out.println();
        // step 2:
        for (int size = arr.length; size >1; size--) {
            swap(arr, 0, size - 1);  //每次都把最大的元素交换到最后的位置,然后在前半部分做heap sort,后半部分放sort好的元素，从最后一个元素一个一个的摆
            shiftDown(arr, 0, size - 1);  //size表示图中的那个虚的隔板，对0..size-1的那部分继续sort
        }
    }
    private void heapify(int[] arr) {
        for (int i = arr.length / 2 - 1; i >= 0; i--) {  //这里index是从0开始的，所以最后一个非叶子节点是index2-1, 从最后一个爸爸开始做percolate down
            shiftDown(arr, i, arr.length);
        }
    }
    private void shiftDown(int[] arr, int index, int len) {
        while (index <len) {
            int max = index;

            int left = index * 2 +1;
            int right = index * 2 +2;
            // find the maximum of left and right
            if (left <len && arr[left] > arr[max]) {  //先看左孩子
                max = left;
            }
            if (right < len && arr[right] > arr[max]) { //如果有右孩子看右孩子
                max = right;
            }
            // check if it is cur itself
            if (max == index) break;
            swap(arr, index, max);
            index = max;
        }
    }
    private void swap(int[] arr, int a, int b) {
        int tmp = arr[a];
        arr[a] = arr[b];
        arr[b] = tmp;
    }
}

```