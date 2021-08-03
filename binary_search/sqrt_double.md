这题有坑
这题是在连续search range上做binary search


num == 1 :return 1
num < 1 : [num，1]
num > 1:  [1, num]


what is the termination condition?
定义一个误差范围，应该是一个相对数值，相当于number的比例应该是固定的


```java
public‌ ‌double‌ ‌sqrt(double‌ ‌num,‌ ‌double‌ ‌epsilon)‌ ‌{‌ ‌
    if‌ ‌(num‌ ‌==‌ ‌1)‌ ‌return‌ ‌1;‌ ‌
    double‌ ‌left‌ ‌=‌ ‌1;‌ ‌
    double‌ ‌right‌ ‌=‌ ‌num;‌ ‌
    if‌ ‌(num‌ ‌<‌ ‌1)‌ ‌{‌ ‌
        left‌ ‌=‌ ‌num;‌ ‌
        right‌ ‌=‌ ‌1;‌ ‌
    }‌ ‌
    while‌ ‌(left‌ ‌<=‌ ‌right)‌ ‌{‌ ‌ ‌
        double‌ ‌mid‌ ‌=‌ ‌left‌ ‌+‌ ‌(‌ ‌right‌ ‌-‌ ‌left‌ ‌)‌ ‌/‌ ‌2;‌ ‌
        double‌ ‌diff‌ ‌=(num‌ ‌-‌ ‌mid‌ ‌*‌ ‌mid)‌ ‌/‌ ‌num;‌ ‌
        if‌ ‌(Math.abs(diff)‌ ‌<=‌ ‌epsilon)‌ ‌{‌ ‌
            return‌ ‌mid;‌ ‌
        }‌  ‌else‌ ‌if‌ ‌(diff‌ ‌<‌ ‌0)‌ ‌{‌ ‌
            right‌ ‌=‌ ‌‌mid‌;‌  //这里不能减1,因为是实数
        }‌ ‌else‌ ‌{‌ ‌
            left‌ ‌=‌ ‌‌mid‌;‌ ‌
        }‌ ‌
    }‌ ‌
    return‌ ‌0;‌ ‌
}‌ 

```



