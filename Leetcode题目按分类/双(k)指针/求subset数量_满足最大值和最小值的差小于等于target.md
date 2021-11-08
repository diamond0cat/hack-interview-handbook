- fb phone screen


- 我们只关心subset的最大值，最小值
- 
- 怎么对subsets分类? ==> 固定最大值

 ‌
- 分‌解‌所‌有‌满‌足‌要‌求‌的‌subset‌ ‌
 - 固‌定‌subset‌的‌最‌大‌值‌ ‌j‌ ‌

- for‌ ‌j:‌ ‌
  - #‌ ‌of‌ ‌subsets‌ ‌using‌ ‌array[j]‌ ‌as‌ ‌the‌ ‌max‌ ‌value.‌ ‌
  - -->‌ ‌find‌ ‌the‌ ‌i‌ ‌as‌ ‌the‌ ‌min(min‌ ‌value)‌ ‌for‌ ‌the‌ ‌subset‌ ‌
  - <‌ ‌==‌ ‌>‌ ‌sorted‌ ‌array,‌  ‌for‌ ‌j,‌ ‌find‌ ‌the‌ ‌leftmost‌ ‌i‌ ‌such‌ ‌that‌ ‌array[j]‌ ‌-‌ ‌array[i]‌ ‌<=‌ ‌target.‌ ‌
 ‌

-‌ ‌Choice‌ ‌1:‌ ‌binary‌ ‌search‌ ‌
-‌ ‌Choice‌ ‌2:‌ ‌two‌ ‌pointers(2diff)‌ ‌
 ‌

 - 1 3 5 6 8  
 -   i   j
 -   可选可不选3,可选可不选5,6必须选  （求的是以6为max的subsets的数量，[3,5]可以选空集，然后跟6组合，就只剩6一个，也算进去）
```java 
int‌ ‌count‌ ‌=‌ ‌0;‌ ‌
int‌ ‌left‌ ‌=‌ ‌0;‌ ‌
int‌ ‌right‌ ‌=‌ ‌0;‌ ‌//‌ ‌we‌ ‌can‌ ‌not‌ ‌ignore‌ ‌index‌ ‌0‌ ‌as‌ ‌right‌ ‌in‌ ‌this‌ ‌case.‌ ‌这个corner case需要跟interviewer clarify,这个subset能不能只包含一个元素，它自己既是max也是min
while‌ ‌(right‌ ‌<‌ ‌array.length)‌ ‌{‌ ‌
  if‌ ‌(array[right]‌ ‌-‌ ‌array[left]‌ ‌>‌ ‌target)‌ ‌{‌ ‌
    left++;‌ ‌
  }‌ ‌else‌ ‌{‌ ‌
     count‌ ‌+=‌ ‌1‌ ‌<<‌ ‌(right‌ ‌-‌ ‌left);//‌ ‌2^(right‌ ‌-‌ ‌left);‌ ‌//这里要求的是array[j]作为max的所有与的subsets
     right++;‌ ‌
  }‌ ‌
}‌ ‌

```