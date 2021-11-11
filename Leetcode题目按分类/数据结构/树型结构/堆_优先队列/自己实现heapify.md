heapify的过程：

从最后一个非叶子节点开始，倒着做shiftDown

如何定位最后一个非叶子节点？只要拿到最后一个节点的索引，然后找最后一个节点的父亲

parent(getNode(size - 1))

```java
public MaxHeap(E[] arr){
    data = new Array<>(arr);
    if(arr.length != 1){
        for(int i = parent(arr.length - 1) ; i >= 0 ; i --)
            siftDown(i);
        }
    }
}


    private void siftDown(int k){  //把k跟它的左右孩子中较大的那个交换

        while(leftChild(k) < data.getSize()){ //k还有孩子的情况,至少还有一个孩子
            int j = leftChild(k); // 在此轮循环中,data[k]和data[j]交换位置
            if( j + 1 < data.getSize() &&
                    data.get(j + 1).compareTo(data.get(j)) > 0 )  //如果左孩子的值小于右孩子的值
                j ++;  //j指到右孩子 等价于 j = rightChild(k)
            // data[j] 是 leftChild 和 rightChild 中的最大值

            if(data.get(k).compareTo(data.get(j)) >= 0 ) //k比j大，不用继续了，k比它的左右两个孩子都大
                break;

            data.swap(k, j);  //否则把k跟他的孩子交换
            k = j;  //k指向新的位置，继续下沉
        }
    }


    // 返回完全二叉树的数组表示中，一个索引所表示的元素的父亲节点的索引
    private int parent(int index){
        if(index == 0)
            throw new IllegalArgumentException("index-0 doesn't have parent.");
        return (index - 1) / 2;
    }


```
