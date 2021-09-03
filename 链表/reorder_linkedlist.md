

```
Reorder the given singly-linked list N1 -> N2 -> N3 -> N4 -> … -> Nn -> null to be N1- > Nn -> N2 -> Nn-1 -> N3 -> Nn-2 -> … -> null

Examples

L = null, is reordered to null
L = 1 -> null, is reordered to 1 -> null
L = 1 -> 2 -> 3 -> 4 -> null, is reordered to 1 -> 4 -> 2 -> 3 -> null
L = 1 -> 2 -> 3 -> null, is reordred to 1 -> 3 -> 2 -> null

```


    // odd number or even number
    // Steps: 1. find mid node(discuss for odd and even number) 
    // 2. cut half of the linked list 
    // 3. reverse second half 
    // 4. merge two linked list


```java
/**
 * class ListNode {
 *   public int value;
 *   public ListNode next;
 *   public ListNode(int value) {
 *     this.value = value;
 *     next = null;
 *   }
 * }
 */
public class Solution {
  public ListNode reorder(ListNode head) {
    // Write your solution here.
    if (head == null || head.next == null) {
      return head;
    }
    
    // find middle
    ListNode middle = findMiddle(head);
    ListNode firstHalf = head;
    ListNode secondHalf = middle.next;
    
    middle.next = null;
    // reverse second half
    secondHalf = reverse(secondHalf);
    // merge two half
    return merge(firstHalf, secondHalf);
    
    
    
  }
  
  public ListNode merge(ListNode list1, ListNode list2) {
    ListNode dummy = new ListNode(-1);
    ListNode tail = dummy;
    while (list1 != null && list2 != null) {
      tail.next = list1;
      list1 = list1.next;
      tail.next.next = list2;
      list2 = list2.next;
      tail = tail.next.next;
    }
    if (list1 != null) {
      tail.next = list1;
    }
    if (list2 != null) {
      tail.next = list2;
    }
    return dummy.next;
  }
  
  public ListNode findMiddle(ListNode head) {
    if (head == null || head.next == null) {
      return head;
    }
    ListNode slow = head;
    ListNode fast = head;
    while (fast.next != null && fast.next.next != null) {
      slow = slow.next;
      fast = fast.next.next;
    }
    return slow;
  }
  
  public ListNode reverse(ListNode head) {
    if (head == null || head.next == null) {
      return head;
    }
    ListNode prev = null;
    ListNode cur = head;
    while (cur != null) {
      ListNode next = cur.next;
      cur.next = prev;
      prev = cur;
      cur = next;
    }
    return prev;
    /*
    ListNode newHead = reverse(head.next);
    head.next.next = newHead;
    newHead.next = null;
    return newHead; */
  }
}

```
