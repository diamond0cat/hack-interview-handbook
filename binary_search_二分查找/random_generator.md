


how to model input?  

weight -->uniform  how?

40+30+20+10 = 100

binary search不是最直接的方法，最直接的方法是new一个长度是total weight的数组，
00-39放a
40-69 放b



![20210801140118](https://i.loli.net/2021/08/02/1cdLGIur2ZQ6CHe.png)
```java
class‌ ‌RandomGenerator‌ ‌{‌ ‌
    private‌ ‌int[]‌ ‌ranges;‌ ‌
    private‌ ‌final‌ ‌String[]‌ ‌symbols;‌ ‌
    private‌ ‌Random‌ ‌random;‌ ‌
    ‌
    ‌public‌ ‌RandomGenerator(String[]‌ ‌symbols,‌ ‌int[]‌ ‌weights)‌ ‌{‌ ‌
        ‌//‌ ‌validation‌ ‌@‌ ‌constructor‌ ‌
        this.symbols‌ ‌=‌ ‌symbols;‌  ‌//‌ ‌clone.‌ ‌
        this.random‌ ‌=‌ ‌new‌ ‌Random();‌ ‌
        ranges‌ ‌=‌ ‌new‌ ‌int[weights.length];‌ ‌
        ranges[0]‌ ‌=‌ ‌weights[0];‌ ‌
        for‌ ‌(int‌ ‌i‌ ‌=‌ ‌1;‌ ‌i‌ ‌<‌ ‌weights.length;‌ ‌i++)‌ ‌{‌ ‌
            ranges[i]‌ ‌=‌ ‌ranges[i‌ ‌-‌ ‌1]‌ ‌+‌ ‌weights[i];‌ ‌
        }‌ ‌
    }‌ ‌
    public‌ ‌String‌ ‌getRandom()‌ ‌{‌ ‌
        int‌ ‌randomWeight‌ ‌=‌ ‌random.nextInt(ranges[ranges.length‌ ‌-‌ ‌1]);‌ ‌
        return‌ ‌symbols[binarySearch(randomWeight)];‌ ‌
    }‌ ‌

    private‌ ‌int‌ ‌binarySearch(int‌ ‌randomWeight)‌ ‌{‌ ‌
        int‌ ‌left‌ ‌=‌ ‌0;‌ 
        int‌ ‌right‌ ‌=‌ ‌ranges.length‌ ‌-‌ ‌1;‌ ‌
        while‌ ‌(left‌ ‌<‌ ‌right)‌ ‌{‌ ‌
           int‌ ‌mid‌ ‌=‌ ‌left‌ ‌+‌ ‌(right‌ ‌-‌ ‌left)‌ ‌/‌ ‌2;‌ ‌
           if‌ ‌(ranges[mid]‌ ‌>‌ ‌randomWeight)‌ ‌{‌ ‌
              right‌ ‌=‌ ‌mid;‌ ‌
             }‌ ‌else‌ ‌{‌ ‌
              left‌ ‌=‌ ‌mid‌ ‌+‌ ‌1;‌ ‌
           }‌ ‌
        }‌ ‌
        return‌ ‌left;‌ ‌
    }‌ ‌
}‌ ‌
 ‌
```