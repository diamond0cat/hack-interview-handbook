


```
              root‌ ‌=‌ ‌0‌ ‌
                  ‌/‌ ‌
                 ‌1‌  ‌ ‌
                 ‌/‌            ‌\‌ ‌
               ‌ ‌2‌               ‌3‌ ‌
               ‌/‌  ‌\‌             ‌/‌   ‌\‌ ‌
          4‌ ‌=a‌‌ ‌  ‌5‌       ‌6‌    ‌ ‌ ‌7‌ ‌=‌ ‌b‌ ‌
          /‌ ‌\‌ ‌
        ‌8‌ ‌   ‌‌9‌ ‌=‌ ‌a‌ ‌
 ‌
class‌ ‌TreeNode‌ ‌{‌ ‌
int‌ ‌value;‌ ‌
TreeNode‌ ‌left;‌ ‌
TreeNode‌ ‌right;‌ ‌
‌TreeNode‌ ‌parent;‌ ‌
}‌ ‌
 ‌
Solution‌ ‌1:‌ ‌ ‌
Step‌ ‌1:‌ ‌From‌ ‌a,‌ ‌keep‌ ‌looking‌ ‌up,‌ ‌and‌ ‌store‌ ‌all‌ ‌ancestors‌ ‌of‌ ‌a‌ ‌to‌ ‌a‌ ‌HashSet‌ ‌{9‌ ‌4‌ ‌2‌ ‌1}.‌ ‌
Step‌ ‌2:‌ ‌From‌ ‌b,‌ ‌keep‌ ‌looking‌ ‌up‌ ‌one‌ ‌by‌ ‌one,‌ ‌until‌ ‌we‌ ‌find‌ ‌the‌ ‌current‌ ‌node‌ ‌is‌ ‌in‌ ‌the‌ ‌HashSet.‌ ‌
 ‌
Time‌ ‌=‌ ‌O(2‌ ‌*‌ ‌height)‌ ‌<=‌ ‌O(n)‌ ‌
Space‌ ‌=‌ ‌O(height)‌ ‌<=‌ ‌O(n)‌ ‌
 ‌
Solution‌ ‌2:‌ ‌
Step‌ ‌1:‌ ‌keep‌ ‌looking‌ ‌up‌ ‌from‌ ‌a‌ ‌and‌ ‌b‌ ‌respectively,‌ ‌to‌ ‌find‌ ‌depth(a)‌ ‌and‌ ‌depth(b).‌ ‌
Step‌ ‌2:‌ ‌trace‌ ‌up‌ ‌from‌ ‌the‌ ‌deeper‌ ‌one.‌ ‌move‌ ‌|depth(a)‌ ‌-‌ ‌depth(b)|.‌ ‌
Step‌ ‌3:‌ ‌move‌ ‌a‌ ‌and‌ ‌b‌ ‌together‌ ‌one‌ ‌step‌ ‌by‌ ‌one‌ ‌step,‌ ‌until‌ ‌a‌ ‌==‌ ‌b.‌ ‌
 ‌
Time‌ ‌=‌ ‌O(height)‌ ‌
Space‌ ‌=‌ ‌O(1)‌

```