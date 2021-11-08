


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
        if (output.isEmpty()) move();
        return output.pollFirst();
    }
    
    /** Get the front element. */
    public int peek() {
      if (output.isEmpty()) move();
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

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
 ```