
an algorithm called Reservoir sampling which is a family of randomized algorithms for sampling from a population of unknown size.


```
Consider an unlimited flow of data elements. How do you sample one element from this flow, such that at any point during the processing of the flow, you can return a random element from the n elements read so far.

You will implement two methods for a sampling class:

read(int value) - read one number from the flow
sample() - return at any time the sample, if n values have been read, the probability of returning any one of the n values is 1/n, return null(Java)/INT_MIN(C++) if there is no value read so far
You may need to add more fields for the class.
```

//不允许存东西，也不知道input有多长

```java
class Stream {
  // returns null if the stream ends
  public Element getNext() {};
}

void sample(Stream s) {
  Element sample = null;
  Element tmp = s.getNext();

  // count is the number of elements read so far
  int coutn = 1;
  Random random = new Random();

  while (tmp != null) {
    int prob = random.nextInt(count);  //第一次100%的概率赋给sample,第二次50%的概率赋给sample,第三个数进来以33$的概率赋给sample
    if (prob == 0) {  //一开始进来的时候count=0, random(1)的结果只可能是0
      sampel = tmp;
    }
    tmp = s.getNext();
    count++;
  }
}


```


```java
public class Solution {
  private int count;
  private Integer sample;

  public Solution() {
    // Write your constructor code here if necessary.
    this.count = 0;   //记录现在读进来几个数， number of elements read so far
    this.sample = null;  //要返回的sample出来的结果
  }
  
  public void read(int value) {
    // Write your implementation here.
    count++;
    int prob = (int)(Math.random() * count);   //生成 [0, count-1]之间的数
    if (prob == 0)  {   //这句话比较精巧，这样在count==0的时候也能返回0  
      sample = value;
    }
  }
  
  public Integer sample() {
    // Write your implementation here.
    return sample;
  }
}

```


### 扩展一下，取k个样本:

Reservior samplging is a  family of randomized algorithms for randomly choosing a sample of K items from a list S containing n items, where n is either a very large or unknown number. typically n is large enough that the list doesn't fit into main memory and it is fed as a stream.

stream.getNext()
count <= k  samples.add(element)  // samples是一个长度为k的数组, Element[] samples - new Element[k];

k = 100

samples0, samples1, ....samples99
以100/101的概率把x保留下来
  如果决定把x保留下来，那么在已有的sampels中随机枪毙一个人

以100/102的概率把y保留下来
  如果决定把y保留下来，那么在已有的samples中随机枪毙一个人


induction:数学归纳法
P(a1 in samples) = 100%
P(a2 in samples) = 100%
P(a3 in samples) = 100%
...
P(a100 in samples) = 100%

第101步开始：
P(a101 in samples) = 100/101
P(在101步开始, a1 in samples) = 
  P(在100步，a1 in samples) * (在101步，a1没有被枪毙)
= 100%                     *  （1 - P(在101步a1被枪毙)）
= 100% * (1- 100/101 * 1/100) = 100/ 101

条件1: 选择把a101保留下来 ==> 100/101
条件2：100个人供枪毙，凭什么枪毙a1 ==> 1/100




P(a1 in samples) = P(a2 in samples)= P(a3 in samples)=...



第102步开始：
P(a102 in samples) = 100/102
P(在102步开始, a1 in samples) = 
  P(在101步，a1 in samples) * (在102步，a1没有被枪毙)
= 100/101 * (1- 100/102 * 1/100) = 100/101 * (1- 1/102)=100/101 * 101/102
 = 100/102


 ### what if we ask you to return a random largest number

 for example, given a stream like "1 2 5a 3 4 3 4 5b" you may return 4a or 5b randomly

 data structure:

 count = 存的是max value的个数

initialize:
 samples = getNext();
 count = 1

for each step:
temp = getNext()
if (temp.key < sample.key>) ignore, do nothing
else if (temp.key > sample.key) {
   sample = temp;  //更新最大值
   count = 1;
} else if (temp.key == sample.key) {   //这一步里面跟question 1是一模一样的
  count++;  
  以1/count的概率将sample赋值为temp
}


```java
public class Solution {
  private final int k;
  private int count;
  private List<Integer> sample;
  
  public Solution(int k) {
    // Complete the constructor if necessary.
    if (k < 0) {
      throw new IllegalArgumentException("k must be > 0");
    }
    this.k = k;
    this.count = 0;
    sample = new ArrayList<Integer>();
  }
  
  public void read(int value) {
    // Write your implementation here.
    count++;
    if (count <= k) {
      sample.add(value);
    } else {
      int random = (int)(Math.random() * count);
      if (random < k) {
        sample.set(random, value);
      }
    }
  }
  
  public List<Integer> sample() {
    // Write your implementation here.
    return sample;
  }
}

```



 