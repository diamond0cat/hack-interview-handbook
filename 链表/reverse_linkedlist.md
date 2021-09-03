

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null ||head.next == null) return head;
        
        ListNode prev = null;
        
        while (head != null) {
            ListNode next = head.next;
            head.next = prev;
            prev = head;
            head = next;
        }
        return prev;
    }
}
```
![picture 2](https://i.loli.net/2021/09/04/3DPCqpMVG9mFu1s.png)  


 ```java
 class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null ||head.next == null) return head;  //head.next要判空，因为后面有一行:head.next.next = head
        
        ListNode newHead = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return newHead;
    }

}
```
![picture 1](https://i.loli.net/2021/09/04/koUNamzs4hEKSvF.png)  

