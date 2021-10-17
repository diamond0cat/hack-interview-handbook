

```java
  public RandomListNode copy(RandomListNode head) {
    // Write your solution here.
    if (head == null) {
      return null;
    }

    // 初始化
    RandomListNode newHead = new RandomListNode(head.value);
    // 建立一个map防止重复拷贝节点， key: originao node. value: copied node，存的一一对应的关系
    Map<RandomListNode, RandomListNode> lookup = new HashMap<>();
    lookup.put(head, newHead);
    RandomListNode cur = newHead;

    while (head != null) {  // cur is always head's copy , 链表用一个循环走一遍
      if (head.next != null) {
        if (!lookup.containsKey(head.next)) {
          lookup.put(head.next, new RandomListNode(head.next.value));
        }
        cur.next = lookup.get(head.next);  //如果节点已经考过了不用再考，连一下
      }
      if (head.random != null) {
        if (!lookup.containsKey(head.random)) {
          lookup.put(head.random, new RandomListNode(head.random.value));
        }
        cur.random = lookup.get(head.random);
      }
      head = head.next;
      cur = cur.next;

    }
    return newHead;
  }
  ```