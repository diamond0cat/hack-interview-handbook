初始想法是用两个stack实现,但是如果有一种case的时间复杂度会很差

1000 elements in stack2:

1st call: left.remove(): 1000 stack2.pop + 1000 stack2.push + 1.stack1.pop = 2001
2nd call: right.remove(): 999 stack1.pop + 999 stack2.push + 1.stack2.pop 1999
3rd call:  left.remove() : 998 + 998 + 1....


这种情况不存在amortized time,还是O(n)的时间复杂度
为什么这种情况下时间复杂度差? 因为每次要实现pop，都要把数据全倒出去再塞到另一个栈

怎么解决？ 借用一个buffer,并且让两个栈里的数据比较平均
instead of moving all elements form one stack to the other, we just move half elements

需要使用三个栈：





