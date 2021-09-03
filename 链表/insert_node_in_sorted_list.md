insert a node in a sorted linkedlist:
1->3-->6-->9-->null  target = 7 or 10 or 0


use a dummy node

```java
  public ListNode insert(ListNode head, int value) {
    // 1. find first node which is >= value
    ListNode dummy = new ListNode(-1);
    dummy.next = head;
    ListNode prev = dummy;
    ListNode cur = head;

    while (cur != null && cur.value < value) {
      prev = cur;
      cur = cur.next;
    }
    // cur == null || cur.val >= value
    prev.next = new ListNode(value);
    prev.next.next = cur;
    return dummy.next;
  }
  ```