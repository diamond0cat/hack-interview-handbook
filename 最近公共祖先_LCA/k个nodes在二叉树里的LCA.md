- LCA of k node sin a binary tree (no parent pointers)

- general idea sot olsve k-something

- solution 1: iterative reduction
- time =O(k*n) sapce = O(height)


- solution 2; binary reduction


- soltuion 3: k个nodes一起做LCA

```
物‌理‌意‌义‌：‌LCA(root,‌ ‌nodes)‌ ‌
Case‌ ‌1:‌ ‌if‌ ‌all‌ ‌nodes‌ ‌are‌ ‌under‌ ‌root,‌ ‌return‌ ‌LCA‌ ‌of‌ ‌these‌ ‌nodes‌ ‌
Case‌ ‌2:‌ ‌if‌ ‌a‌ ‌subset‌ ‌of‌ ‌the‌ ‌given‌ ‌nodes‌ ‌are‌ ‌under‌ ‌root,‌ ‌return‌ ‌LCA‌ ‌of‌ ‌the‌ ‌nodes‌ ‌under‌ ‌root‌ ‌
Case‌ ‌3:‌ ‌if‌ ‌none‌ ‌of‌ ‌the‌ ‌nodes‌ ‌are‌ ‌under‌ ‌root,‌ ‌return‌ ‌null‌ ‌

```