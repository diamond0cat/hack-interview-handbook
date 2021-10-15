

```
                10‌ ‌ ‌
      ‌/‌          ‌         \‌ ‌
 ‌    ‌5‌                  ‌15‌ ‌
     ‌/‌  ‌\‌            ‌/‌          ‌\‌ ‌
   2‌   ‌‌7‌‌       ‌‌12=a‌ ‌   ‌    ‌‌20=b‌ ‌ ‌
  /\‌ 
 ‌1‌ ‌ ‌
 ‌
[a‌ ‌=‌ ‌12,‌ ‌b‌ ‌=‌ ‌20]‌ ‌
 ‌
Assume‌ ‌a‌ ‌<‌ ‌b‌ ‌
Key‌ ‌insight‌ ‌1:‌ ‌the‌ ‌value‌ ‌of‌ ‌the‌ ‌LCA‌ ‌must‌ ‌be‌ ‌between‌ ‌a‌ ‌and‌ ‌b‌ ‌
Key‌ ‌insight‌ ‌2:‌ ‌LCA‌ ‌must‌ ‌be‌ ‌the‌ ‌shallowest‌ ‌node‌ ‌whose‌ ‌value‌ ‌is‌ ‌between‌ ‌a‌ ‌and‌ ‌b‌ ‌
 ‌
Algorithm:‌ ‌iterative‌ ‌
case‌ ‌1:‌ ‌if‌ ‌root.value‌ ‌<‌ ‌a,‌ ‌then‌ ‌a‌ ‌and‌ ‌b‌ ‌must‌ ‌be‌ ‌in‌ ‌root's‌ ‌right‌ ‌subtree.‌ ‌therefore,‌ ‌root‌ ‌=‌ ‌root.right‌ ‌
case‌ ‌2:‌ ‌if‌ ‌root.value‌ ‌>‌ ‌b,‌ ‌then‌ ‌a‌ ‌and‌ ‌b‌ ‌must‌ ‌be‌ ‌in‌ ‌the‌ ‌root's‌ ‌left‌ ‌subtree.‌ ‌therefore,‌ ‌root‌ ‌=‌ ‌root.left‌ ‌
case‌ ‌3:‌ ‌a‌ ‌<=‌ ‌root.value‌ ‌<=‌ ‌b,‌ ‌then‌ ‌return‌ ‌root‌ ‌


```