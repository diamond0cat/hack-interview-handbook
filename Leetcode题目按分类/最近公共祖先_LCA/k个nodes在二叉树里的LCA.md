- LCA of k node sin a binary tree (no parent pointers)

- general idea sot olsve k-something

- solution 1: iterative reduction
- time =O(k*n) sapce = O(height)


- solution 2; binary reduction


- soltuion 3: k个nodes一起做LCA

```
物‌理‌意‌义‌：‌LCA(root,‌ ‌nodes)‌ ‌  (nodes = list of target nodes  / set of target nodes )
Case‌ ‌1:‌ ‌if‌ ‌all‌ ‌nodes‌ ‌are‌ ‌under‌ ‌root,‌ ‌return‌ ‌LCA‌ ‌of‌ ‌these‌ ‌nodes‌ ‌
Case‌ ‌2:‌ ‌if‌ ‌a‌ ‌subset‌ ‌of‌ ‌the‌ ‌given‌ ‌nodes‌ ‌are‌ ‌under‌ ‌root,‌ ‌return‌ ‌LCA‌ ‌of‌ ‌the‌ ‌nodes‌ ‌under‌ ‌root‌ ‌
Case‌ ‌3:‌ ‌if‌ ‌none‌ ‌of‌ ‌the‌ ‌nodes‌ ‌are‌ ‌under‌ ‌root,‌ ‌return‌ ‌null‌ ‌



```


```java
public‌‌ ‌TreeNode‌ ‌‌LCA‌(TreeNode‌ ‌root,‌ ‌TreeNode‌ ‌a,‌ ‌TreeNode‌ ‌b)‌ ‌{‌ ‌
 ‌‌if‌‌ ‌(root‌ ‌==‌ ‌‌null‌‌ ‌||‌ ‌root‌ ‌==‌ ‌a‌ ‌||‌ ‌root‌ ‌==‌ ‌b)‌ ‌{‌ ‌
   ‌‌return‌‌ ‌root;‌ ‌
 ‌}‌ ‌
 ‌
 ‌TreeNode‌ ‌result‌ ‌=‌ ‌‌null‌;‌ ‌
 ‌‌for‌‌ ‌(TreeNode‌ ‌child‌ ‌:‌ ‌root.children)‌ ‌{‌ ‌‌//‌  ‌step‌ ‌1‌ ‌
   ‌TreeNode‌ ‌subResult‌ ‌=‌ ‌LCA(child,‌ ‌a,‌ ‌b);‌ ‌
   ‌‌if‌‌ ‌(‌subResult‌  ‌!=‌ ‌‌null‌)‌ ‌{‌                  ‌‌//‌ ‌step‌ ‌2‌ ‌
     ‌if‌ ‌(‌result‌  ‌!=‌ ‌null)‌ ‌{‌ ‌
       ‌return‌ ‌root;‌ ‌
     ‌}‌ ‌
     ‌result‌ ‌=‌ ‌subResult;‌ ‌
   ‌}‌ ‌
 ‌}‌ ‌
 ‌‌return‌‌ ‌result;‌                         ‌‌//‌  ‌step‌ ‌3‌ ‌
}‌ ‌
```