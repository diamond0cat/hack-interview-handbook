

```java
public‌‌ ‌TreeNode‌ ‌‌LCA‌(TreeNode‌ ‌root,‌ ‌Set<TreeNode> nodes)‌ ‌{‌ ‌
   // corner case
 ‌
 ‌TreeNode‌ ‌result‌ ‌=‌ ‌‌null‌;‌ ‌
 ‌‌for‌‌ ‌(TreeNode‌ ‌child‌ ‌:‌ ‌root.children)‌ ‌{‌ ‌‌//‌  ‌step‌ ‌1‌ ‌
   ‌TreeNode‌ ‌subResult‌ ‌=‌ ‌LCA(child,‌ nodes);‌ ‌
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