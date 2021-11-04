物理意义：
 max heap: the smaller half
 min heap: the larger half

property #1: max(max heap) <= min(min heap)
property #2: 
  size(max heap) == size(min heap)
  size(max heap) = size(min heap) + 1


algorithM
intiialize; min heap={} max heap={}
for each step(x):
  - case 1: x <= max(max heap) max_heap.insert(x)
    - if size(max_heap)  > size(min_heap) + 1
      - int y = max_heap.pop_max()
      - min_heap.insert(y)
  - case 2: x > max(min heap) , min_heap.insert(x)
    - if size(max_heap) < size(min_heap)
      - int y = min_heap.pop_min()
        - max.heap.insert(y)

```java
public class Solution {
  private PriorityQueue<Integer> smallerHalf;
  private PriorityQueue<Integer> largerHalf;

  public Solution() {
    largerHalf = new PriorityQueue<Integer>();
    smallerHalf = new PriorityQueue<Integer>(11, Collections.reverseOrder());
    // add new fields and complete the constructor if necessary.
  }
  
  public void read(int value) {
    // write your implementation here.
    if (smallerHalf.isEmpty() || value <= smallerHalf.peek()) {
      smallerHalf.offer(value);
    } else {
      largerHalf.offer(value);
    }

    if (smallerHalf.size() - largerHalf.size() >= 2) {
      largerHalf.offer(smallerHalf.poll());
    } else if (largerHalf.size() > smallerHalf.size()) {
      smallerHalf.offer(largerHalf.poll());
    }
  }
  
  public Double median() {
    // write your implementation here.
   int size = size();
   if (size == 0) {
     return null;
   } else if (size % 2 != 0) {
     return (double)(smallerHalf.peek());
   } else {
     return (smallerHalf.peek() + largerHalf.peek()) / 2.0;
   }
  }
  private int size() {
    return smallerHalf.size() + largerHalf.size();
  }
}
``


### follow-up:
  - 数据量很大，内存存不下