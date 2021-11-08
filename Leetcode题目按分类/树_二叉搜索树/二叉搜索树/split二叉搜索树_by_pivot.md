
![picture 2](https://i.loli.net/2021/10/25/ojBKRSUwhTbI8LE.png)  


```
Method‌ ‌1‌ ‌-‌ ‌naive:‌  ‌in‌ ‌sorted‌ ‌array:‌ ‌
1.‌ ‌find‌ ‌the‌ ‌pivot‌ ‌to‌ ‌partition‌ ‌the‌ ‌sorted‌ ‌array‌ ‌to‌ ‌two‌ ‌subarrays.‌ ‌
2.‌ ‌construct‌ ‌two‌ ‌binary‌ ‌search‌ ‌tree‌ ‌from‌ ‌the‌ ‌two‌ ‌subarrays.‌ ‌
extra‌ ‌space.‌ ‌-‌ ‌O(n)‌ ‌
extra‌ ‌time.‌ ‌-‌ ‌O(n)‌ ‌
 ‌
Method‌ ‌2‌ ‌-‌ ‌using‌ ‌the‌ ‌other‌ ‌important‌ ‌properties‌ ‌of‌ ‌the‌ ‌BST‌ ‌
in‌ ‌place:‌  ‌using‌ ‌the‌ ‌derived‌ ‌property‌ ‌of‌ ‌binary‌ ‌search‌ ‌tree.‌ ‌Notice‌ ‌the‌ ‌nodes‌ ‌on‌ ‌the‌ ‌searching‌ ‌path‌ ‌of‌ ‌
pivot
```




```
Method‌ ‌2‌ ‌-‌ ‌using‌ ‌the‌ ‌other‌ ‌important‌ ‌properties‌ ‌of‌ ‌the‌ ‌BST‌ ‌
in‌ ‌place:‌  ‌using‌ ‌the‌ ‌derived‌ ‌property‌ ‌of‌ ‌binary‌ ‌search‌ ‌tree.‌ ‌Notice‌ ‌the‌ ‌nodes‌ ‌on‌ ‌the‌ ‌searching‌ ‌path‌ ‌of‌ ‌
pivot.‌ ‌
259‌ ‌
 ‌
 ‌
                  ‌  ‌‌8‌ ‌
               ‌/‌            ‌\‌ ‌
       ‌      ‌4‌ ‌               ‌‌15‌ ‌
           ‌/‌     ‌\‌         ‌/‌      ‌\‌ ‌
       ‌  ‌1‌       ‌7‌ ‌     ‌ ‌‌9‌ ‌ ‌       ‌ ‌20‌ ‌
                 ‌/‌      ‌/‌  ‌\‌        ‌/‌   ‌\‌ ‌
               ‌ ‌5‌ ‌    ‌‌8.5‌‌  ‌‌11‌‌      ‌17‌   ‌25‌ ‌
                            ‌/‌ ‌
                        ‌ ‌9.5‌ ‌
‌                           ‌\‌ ‌ 
‌                          ‌10.2‌ ‌
 ‌
9‌ ‌is‌ ‌larger‌ ‌than‌ ‌8,‌ ‌we‌ ‌can‌ ‌directly‌ ‌connect‌ ‌it‌ ‌as‌ ‌the‌ ‌right‌ ‌subtree‌ ‌of‌ ‌8.‌ ‌
9.5‌ ‌is‌ ‌larger‌ ‌than‌ ‌9,‌ ‌we‌ ‌can‌ ‌directly‌ ‌connect‌ ‌it‌ ‌as‌ ‌the‌ ‌right‌ ‌subtree‌ ‌of‌ ‌9.‌ ‌
so‌ ‌on...‌ ‌
                  ‌  ‌ 8‌ ‌
               ‌/‌           ‌\‌ ‌
       ‌      ‌4‌ ‌          ‌  ‌‌9‌ ‌
           ‌/‌     ‌\‌        ‌/‌    ‌\‌ ‌ ‌
       ‌  ‌1‌       ‌7‌ ‌     ‌‌8.5‌   ‌ ‌9.5‌ ‌
                 ‌/‌ ‌ ‌
               ‌ ‌5‌ ‌
 ‌
We‌ ‌are‌ ‌always‌ ‌concatenating‌ ‌the‌ ‌subtrees‌ ‌on‌ ‌the‌ ‌rightmost‌ ‌path.‌ ‌
when‌ ‌construct‌ ‌T1:‌ ‌need‌ ‌to‌ ‌maintain‌ ‌two‌ ‌variables:‌ ‌
the‌ ‌root‌ ‌of‌ ‌T1‌ ‌
the‌ ‌largest‌ ‌node‌ ‌of‌ ‌T1‌ ‌
 ‌```

 ```java
 ‌
//‌ ‌all‌ ‌the‌ ‌nodes‌ ‌<=‌ ‌pivot‌ ‌in‌ ‌T1‌ ‌and‌ ‌other‌ ‌nodes‌ ‌in‌ ‌T2.‌ ‌
public‌ ‌TreeNode[]‌ ‌partition(TreeNode‌ ‌root,‌ ‌int‌ ‌pivot)‌ ‌{‌ ‌
 ‌TreeNode[]‌ ‌roots‌ ‌=‌ ‌new‌ ‌TreeNode[2];‌ ‌
 ‌TreeNode‌ ‌largestT1‌ ‌=‌ ‌null;‌ ‌   //小的那个subtree的最大的node
 ‌TreeNode‌ ‌smallestT2‌ ‌=‌ ‌null;‌ ‌  // 大的那个subtree的最小的node
 ‌while‌ ‌(root‌ ‌!=‌ ‌null)‌ ‌{‌ ‌
   ‌if‌ ‌(root.val‌ ‌<=‌ ‌pivot)‌ ‌{‌ ‌
     ‌if‌ ‌(roots[0]‌ ‌==‌ ‌null)‌ ‌{‌  ‌//‌ ‌roots[0]‌ ‌record‌ ‌the‌ ‌root‌ ‌of‌ ‌T1.‌ ‌
       ‌roots[0]‌ ‌=‌ ‌root;‌ ‌
     ‌}‌ ‌else‌ ‌{‌ ‌
       ‌largestT1.right‌ ‌=‌ ‌root;‌  ‌//‌ ‌if‌ ‌T1‌ ‌already‌ ‌exists,‌ ‌just‌ ‌append‌ ‌to‌ ‌its‌ ‌most‌ ‌right‌ ‌node.‌ ‌
     ‌}‌ ‌
     ‌largestT1‌ ‌=‌ ‌root;‌  ‌//‌ ‌update‌ ‌the‌ ‌most‌ ‌right‌ ‌node‌ ‌in‌ ‌T1.‌ ‌
     ‌root‌ ‌=‌ ‌root.right;‌ ‌
   ‌}‌ ‌else‌ ‌{‌ ‌
     ‌if‌ ‌(roots[1]‌ ‌==‌ ‌null)‌ ‌{‌ ‌

 ‌
       ‌roots[1]‌ ‌=‌ ‌root;‌ ‌
     ‌}‌ ‌else‌ ‌{‌ ‌
       ‌smallestT2.left‌ ‌=‌ ‌root;‌ ‌
     ‌}‌ ‌
     ‌smallestT2‌ ‌=‌ ‌root;‌ ‌
     ‌root‌ ‌=‌ ‌root.left;‌ ‌
   ‌}‌ ‌
 ‌}‌ ‌
 ‌//‌ ‌be‌ ‌careful‌ ‌and‌ ‌delink‌ ‌necessary‌ ‌nodes.‌ ‌
 ‌if‌ ‌(largestT1‌ ‌!=‌ ‌null)‌ ‌{‌ ‌
   ‌largestT1.right‌ ‌=‌ ‌null;‌ ‌  // 要把最后的连接断开, 这个例子里的9.5和10.2要断开
 ‌}‌ ‌
 ‌if‌ ‌(smallestT2‌ ‌!=‌ ‌null)‌ ‌{‌ ‌
   ‌smallestT2.left‌ ‌=‌ ‌null;‌ ‌
 ‌}‌ ‌
 ‌return‌ ‌roots;‌ ‌
}‌ ‌
 ‌
assuming‌ ‌balanced‌ ‌binary‌ ‌search‌ ‌tree:‌ ‌
time‌ ‌complexity:‌ ‌O(logn)‌ ‌
space‌ ‌complexity:‌ ‌O(1)‌ ‌
 ‌

```