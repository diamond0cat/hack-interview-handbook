LCA for two nodes a and b in a very large tree that contains billions of nodes

- assume the size of the tree is 32GB and the machine has only 1GB memory available
- assume the tree is roughly balanced
- assume a and b are both in the tree


![picture 1](https://i.loli.net/2021/10/16/msbrZpXTUQEgdvF.png)  

- 整个树有32gb,如何划分：

M1, M2, ...M32下面的子树都大约是一个G


- first do a BFS-1 to search the first 5 levels for a and b:
- Case‌ ‌1:‌ ‌if‌ ‌a‌ ‌and‌ ‌b‌ ‌are‌ ‌both‌ ‌within‌ ‌the‌ ‌first‌ ‌five‌ ‌levels：
    - ‌ ‌LCA(root,‌ ‌a,‌ ‌b,‌ ‌level,‌ ‌levelLimit)‌ ‌  前5层
    ```
    if (level < 5) return null;
    if (root == null || root == a || root == b) {...}
    ```
- Case‌ ‌2:‌ ‌if‌ exactly ‌one‌ ‌of‌ ‌a‌ ‌and‌ ‌b‌ ‌is‌ ‌within‌ ‌the‌ ‌first‌ ‌five‌ ‌levels‌ ‌(assume‌ ‌a‌ ‌is‌ ‌within‌ ‌the‌ ‌first‌ ‌5‌ ‌levels)‌ ‌
  ‌- Find‌ ‌b‌ ‌in‌ ‌the‌ ‌subtree‌ ‌under‌ ‌M1,‌ ‌M2,‌ ‌...,‌ ‌M32‌ ‌
  ‌- Say‌ ‌b‌ ‌is‌ ‌in‌ ‌the‌ ‌subtree‌ ‌under‌ ‌M7‌ ‌
  ‌  - LCA(root,‌ ‌M7,‌ ‌a)‌ ‌

- Case‌ ‌3:‌ ‌if‌ ‌neither‌ ‌of‌ ‌them‌ ‌are‌ ‌within‌ ‌the‌ ‌first‌ ‌five‌ ‌levels,‌ ‌
 ‌   - r0‌ ‌=‌ ‌LCA(M1,‌ ‌a,‌ ‌b),‌ ‌r1‌ ‌=‌ ‌LCA(M2,‌ ‌a,‌ ‌b)‌ ‌.....‌ ‌r31‌ ‌=‌ ‌LCA(M32,‌ ‌a,‌ ‌b)‌ ‌
 ‌   - Case‌ ‌3.1:‌ ‌if‌ ‌all‌ ‌the‌ ‌Rs‌ ‌are‌ ‌null,‌ ‌return‌ ‌nul‌ ‌
 ‌   - Case‌ ‌3.2:‌ ‌if‌ ‌one‌ ‌of‌ ‌the‌ ‌Rs‌ ‌(say‌ ‌r7)‌ ‌is‌ ‌non-null,‌ ‌return‌ ‌r7‌ ‌
 ‌   - Case‌ ‌3.3:‌ ‌if‌ ‌two‌ ‌of‌ ‌them‌ ‌are‌ ‌non-null‌ ‌(say‌ ‌r8,‌ ‌r10),‌ ‌return‌ ‌LCA(root,‌ ‌r8,‌ ‌r10,‌ ‌level,‌ ‌levelLimit)‌ ‌
 ‌
Follow-up:‌ ‌What‌ ‌if‌ ‌you‌ ‌want‌ ‌to‌ ‌complete‌ ‌the‌ ‌work‌ ‌faster‌ ‌with‌ ‌multiple‌ ‌machines?‌ ‌ ‌
Mapper:‌ ‌1‌ ‌job‌ ‌→‌ ‌distribute‌ ‌to‌ ‌32‌ ‌(0b100000)‌ ‌machines‌ ‌
Reducer:‌ ‌collect‌ ‌results‌ ‌from‌ ‌each‌ ‌machine‌ ‌to‌ ‌do‌ ‌some‌ ‌aggregation‌ ‌/‌ ‌post-processing‌ ‌

### 可以利用多台机器并行做LCA来加速