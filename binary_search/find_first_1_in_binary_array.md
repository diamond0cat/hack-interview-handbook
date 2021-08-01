

```java
while‌ ‌(left‌ ‌<‌ ‌right)‌ ‌{‌ ‌
    int‌ ‌mid‌ ‌=‌ ‌left‌ ‌+‌ ‌(right‌ ‌-‌ ‌left)‌ ‌/‌ ‌2;‌ ‌
    if‌ ‌(array[mid]‌ ‌==‌ ‌1)‌ ‌{‌ ‌
        right‌ ‌=‌ ‌mid;‌ ‌
    }‌ ‌else‌ ‌{‌ ‌
        left‌  ‌=‌ ‌mid‌ ‌+‌ ‌1;‌ ‌
    }‌ ‌
}‌ ‌
return‌ ‌array[left]‌ ‌==‌ ‌1‌ ‌?‌ ‌left‌ ‌:‌ ‌left‌ ‌+‌ ‌1;‌  ‌//0000000‌    ‌111‌ ‌

``