
### 使用dummy node

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
  public ListNode mergeSort(ListNode head) {
    // Write your solution here
    if (head == null || head.next == null) {
       return head;
    }
    ListNode mid = findMid(head);
    ListNode next = mid.next;
    mid.next = null;

    ListNode left = mergeSort(head);
    ListNode right = mergeSort(next);
    return merge(left, right);
  }
   private ListNode findMid(ListNode head) {
     ListNode fast = head;
     ListNode slow = head;
     while (fast.next != null && fast.next.next != null) {
        fast = fast.next.next;
        slow = slow.next;
     }
     return slow;
   }
   private ListNode merge(ListNode left, ListNode right) {
     ListNode dummy = new ListNode(0);
     ListNode cur = dummy;
     while (left != null && right != null) {
        if (left.value <= right.value) {
          cur.next = left;
          left = left.next;
        } else  {
          cur.next = right;
          right = right.next;
        }
        cur = cur.next;
     }
     if (left != null) {
       cur.next = left;
     }
     if (right != null) {
       cur.next = right;
     }
     return dummy.next;
   }
}

```


### 不用dummy node

```java
public class Solution {
  public ListNode merge(ListNode one, ListNode two) {
    // Write your solution here
    if (one == null) return two;
    if (two == null) return one;

    ListNode cur = null;
    ListNode head = null;

    //determine the head node
    if (one.value <= two.value) {
      cur = one;
      one = one.next;
    } else {
      cur = two;
      two = two.next;
    }

    head = cur;
    while (one != null && two != null) {
      if (one.value <= two.value) {
        cur.next = one;
        one = one.next;
      } else {
        cur.next = two;
        two = two.next;
      }
      cur = cur.next;
    }
    
    if (one != null)  cur.next = one;
    if (two != null) cur.next = two;
    return head;
  }
}
```