### 遍历链表模板
```java
while (head != null)  head = head.next
```


###走k步的模板:
```java
while (head != null) {   //走k-1步
	k--;
	if (k ==0) break;
	head = head.next;
}
return head;
```




##### 把两个节点之间的反过来
```java
   private void reverseList(ListNode head, ListNode end) {
        if (head == end) return;
        ListNode last = head;
        head = head.next;
        // 改每条边，所以需要访问链表
        while (head != end) {
            ListNode nextHead = head.next;
            // 改一条边
            head.next = last;
            // last,head向后移动一位
            last = head;
            head = nextHead;
        }
        end.next = last;
    }

```