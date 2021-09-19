

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