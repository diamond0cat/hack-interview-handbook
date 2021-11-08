Given a linked list and a target value T, partition it such that all nodes less than T are listed before the nodes larger than or equal to target value T. The original relative order of the nodes in each of the two partitions should be preserved.

Examples

L = 2 -> 4 -> 3 -> 5 -> 1 -> null, T = 3, is partitioned to 2 -> 1 -> 4 -> 3 -> 5 -> null


* solution 1: 
  * step 1: allocate two new dummy heads
  * step 2: iteratate over the list, for each element, compare it with the target:
    * if cur.val < target, append to the dummySmall
    * if cur.val >= target, append to the dummyLarge



```java
  public ListNode partition(ListNode head, int target) {
 
    // Write your solution here
    ListNode dummySmallHead = new ListNode(0);
    ListNode dummyLargeHead = new ListNode(0);
    ListNode smallTail = dummySmallHead;
    ListNode largeTail = dummyLargeHead;
    while (head != null) {
      if (head.value < target) {
        smallTail.next = head;
        smallTail = head;
      } else {
        largeTail.next = head;
        largeTail = head;
      }
      head = head.next;
    }
    largeTail.next = null;//断开
    smallTail.next = dummyLargeHead.next;
    return dummySmallHead.next;
  }
  ```