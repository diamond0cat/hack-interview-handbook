
链表+模拟


朴素解法（哨兵技巧）
这是道模拟题，模拟人工竖式做加法的过程：

从最低位至最高位，逐位相加，如果和大于等于 10，则保留个位数字，同时向前一位进 1 如果最高位有进位，则需在最前面补 1。

做有关链表的题目，有个常用技巧：添加一个虚拟头结点（哨兵），帮助简化边界情况的判断。



时间复杂度：$m$ 和 $n$ 分别代表两条链表的长度，则遍历到的最远位置为 $max(m,n)$，复杂度为 $O(max(m,n))$
空间复杂度：创建了 $max(m,n) + 1$ 个节点（含哨兵），复杂度为 $O(max(m,n))$（忽略常数）
注意：事实上还有可能创建 $max(m + n) + 2$ 个节点，包含哨兵和最后一位的进位。但复杂度仍为 $O(max(m,n))$。

```java

    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode prev = dummy;
        int carry = 0;
        
        while (l1 != null || l2 != null || carry != 0) {
            ListNode cur = new ListNode(0);
            int sum = ((l1 == null) ? 0 : l1.val) + ((l2 == null) ? 0 : l2.val) + carry;
            cur.val = sum % 10;
            carry = sum / 10;
            
            // link the new node to the end of new linkedlist and move the tail pointer
            prev.next = cur;
            prev = prev.next;
            
            l1 = (l1 == null) ? l1 : l1.next;
            l2 = (l2 == null) ? l2 : l2.next;
        }
        return dummy.next;
    }
```
current指向当前链表的尾节


```java

    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        int carry = 0;
        ListNode dummy = new ListNode(-1);
        ListNode cur = dummy;
        
        while (l1 != null || l2 != null || carry != 0) {
            int val1 = l1 == null ? 0 : l1.val;
            int val2 = l2 == null ? 0 : l2.val;
            int sum = val1 + val2 + carry;
            
            cur.next = new ListNode(sum % 10);
            carry = sum / 10;
            
            l1 = l1 == null ? null : l1.next;
            l2 = l2 == null ? null : l2.next;
            cur = cur.next;
            
        }
        return dummy.next;
        
    }
```