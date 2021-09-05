三个栈排序：

stack1(input)
stack2(buffer)                 maintain global min
stack3(result)



两个栈排序：
stack1: store all input (unsorted) elements
stack2: left part | right part
        left part: store all output(sorteed) elements
        right part -used  as a buffer for finding the curent smallest element

    stack 1 [
    stack 2: [               globalmin=2 count =2

```java
public class Solution {
    public void stackSorting(Stack<Integer> s1) {
        Stack<Integer> buffer = new Stack<Integer>();
        if (s1 == null ||s1.size() <= 1) return;
        stackSort(s1, buffer); 
    }
    public void stackSort(Stack<Integer> input, Stack<Integer> buffer) {
        // 每次把数从input倒腾到buffer,记下当前轮的max, 最后把max压到buffer栈底，其他的元素放回input,循环n轮，每次都把curMax压到buffer栈底
        while (!input.isEmpty()) {
            int curMax = Integer.MIN_VALUE;
            int count = 0;

            while (!input.isEmpty()) {
                int cur = input.pop();
                if (cur > curMax) {
                    curMax = cur;
                    count = 1;
                } else if (cur == curMax) {
                    count++;
                }
                buffer.push(cur);
            }
            //buffer里的元素倒腾回input,注意不要动buffer栈底已经排好序的元素
            while (!buffer.isEmpty() && buffer.peek() <= curMax) {
                int tmp = buffer.pop();
                if (tmp != curMax) {
                    input.push(tmp);
                }
            }
            while (count-- > 0) {  //当前轮的max放到buffer栈底
                buffer.push(curMax);
            }
        }

        while (!buffer.isEmpty()) {
            input.push(buffer.pop());
        }

    }
}
```