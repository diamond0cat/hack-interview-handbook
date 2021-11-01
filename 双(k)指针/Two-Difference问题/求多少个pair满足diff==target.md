- two sum, 和 two difference问题的做法：固定一个维度，变化另外一个维度


- two diff问题是最简单的sliding window
- 
- target > 0 这个条件给出了，保证right肯定不会跑到left右边
- 所有的变体：

number of pairs == target
-
- number of pairs ==  target
```
1. array is sorted, no duplicate

  分解所有的pair: i < j
    固定j:
      for all j: try to find the left most i such that array[j]-array[j] >= target
        check if there is any i < j, such taht array[j]  array[i] == target

j --> move right
i is guaranteed not moving left (stay or move right),往左移只会让这个diff变大

what if we have duplicates elements?  homework

2. array is unsorted




```


number of pairs > target
-
- 如果固定j:
  - 这个可以找right most i, such athat array[j] - array[i] > target  (找最后一个满足要求的)
  - 等价于找left most i, such that array[j] - array[i] <= target  (找第一个不满足要求的)

- 第一种判断方法
  - 找right most i, such athat array[j] - array[i] > target  (找最后一个满足要求的)

// 下面这种写法corner  case比较多
```java
// find the right most i , array[j]-array[i] > target

int count = 0;
int left = 0;
int right = 1;
while (right < array.length)  {// for each j
  while (left + 1 < right && array[right] - array[left + 1] > target) {  //我们想把left走到最后一个满足条件的位置，所以其实是要判断left的下一个位置，left才能往前走
    left++;
  }
  // we need to handle the case where there is no applicable left for the current right
  if (array[right] - array[left] > target) count += left + 1;
  right++;
}  
return count;

```

- 第二种判断方法
  - 找left most i, such that array[j] - array[i] <= target  (找第一个不满足要求的)


```java

int count = 0;
int left = 0;
int right = 1;

while (right < arr.length) {  // for each j
  if (array[right] - array[left] <= target) {  //如果array[right]-array[left]<=target,我们可以移动j了，同时count+=left, left不算进去
    count += left;
    right++;
  } else {
    left++;     //left移到第一个<=target的位置为止
  }
}
return count;

```

等价于， 上面的写法相当于把里面那层的while拆出来了


```java

int count = 0;
int left = 0;
int right = 1;

while (right < arr.length) {  // for each j
  while (array[right] - array[left] > target) {
     left++；
  } 

  // left = left most array[right]-array[left] <= target
  count += left;
  right++;
  
}
return count;

```


number of pairs > target
-
- 如果固定i, for each i:
  - find the left most j such that array[j]-array[i] > target
  
```java
while (i < array.length) {  //for each i
  while (j < array.length && array[j]-array[i] <= target) {
      j++;
  }
  count += arrray.length - j;
  i++;
}


```



number of pairs < target
-



number of pairs == target, the array is unsorted
-

- 思路：怎么分解：
  - for each j: 
    - j前面所有的element里面有多少个满足 array[j] - array[i]== target 或者 array[j]-array[i] == -target
      - 