


```java
public class Solution {
  public ListNode reverseInPairs(ListNode head) {
    // Write your solution here
    // base case
    if (head == null ||head.next == null) return head;
    ListNode next = head.next;
    head.next = reverseInPairs(head.next.next);
    next.next = head;
    return next;
  }
}

```