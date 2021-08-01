

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