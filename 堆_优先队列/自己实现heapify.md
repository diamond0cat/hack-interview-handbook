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
```
