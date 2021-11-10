
- 什么时候导数据？ y用户要数据的时候导数据
- pop栈没有拿完的时候不能导数据，否则新导的数据会盖在旧数据上面

```java
class MyQueue {
    Deque<Integer> input;
    Deque<Integer> output;

    /** Initialize your data structure here. */
    public MyQueue() {
        input = new ArrayDeque<>();
        output = new ArrayDeque<>();
    }
    
    /** Push element x to the back of queue. */
    public void push(int x) {
        input.offerFirst(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        if (output.isEmpty()) move();   //用户要数据的时候导数据
        return output.pollFirst();
    }
    
    /** Get the front element. */
    public int peek() {
      if (output.isEmpty()) move();  //用户要数据的时候导数据
       return output.peekFirst();
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
       return input.isEmpty() && output.isEmpty();
    }
    private void move() {
       while (!input.isEmpty()) {
           output.offerFirst(input.pollFirst());
       }
    }
}
