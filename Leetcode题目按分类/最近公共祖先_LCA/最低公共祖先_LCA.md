

![picture 11](https://i.loli.net/2021/09/16/FKplv9A2SZQ71HV.png)  


ancestor:自己也算自己的ancestor

- 左子树和右子树干一样的事


5' ancestor: 5, 10, 12
9's ancestor: 9, 7, 5, 10, 12

这题的scope在哪里？  这个题目怎么理解?

- 要讨论清楚所有的情况：
  - case 1:  a and b 直接隶属
    - case 1.1 if left == null && right == null return  null
    - case 1.2  if either left or right returns a non-null value, return it to my parent
  - case 2:  a and b 不直接隶属
    - case 2.1 if left == null && right == null return null     
    - case 2.2 if either left or right returns a non-value, retunr it to my parent
    - case 2.3 if both left and right return non-null, return myself




```java
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        // base case
        if (root == null) return null;
        
        if (root.val == p.val) return root;
        if (root.val == q.val) return root;
        
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p,q);
        
        if (left == null &&right == null) return null;
        else if (left == null || right == null) {
            return left == null ? right : left;   //这里不能直接返回
        } else return root;
        
        
    }
```

## 如果a和b可能不在这棵树里，讨论上面的几种情况：
  - case 1:  a and b 直接隶属
    - case 1.1 if left == null && right == null return  null
    - case 1.2  if either left or right returns a non-null value, return it to my parent
  - case 2:  a and b 不直接隶属
    - case 2.1 if left == null && right == null return null     
    - case 2.2 if either left or right returns a non-value, retunr it to my parent //这种情况可能会有问题,这里不能直接返回itself,
    - case 2.3 if both left and right return non-null, return myself  

1. 返回c的情况下，a和b一定都在树里，而且不直接隶属
2. 

```java
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        // base case
        if (root == null) return null;
        
        if (root.val == p.val) return root;
        if (root.val == q.val) return root;
        
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p,q);
        
        if (left == null &&right == null) return null;
        else if (left == null || right == null) {
            return left == null ? right : left;   //这里不能直接返回另外一边了，需要在check一下，如果b在树里，只可能在a下面，只有a下面没有check过
        } else return root;
        
        
    }


![picture 16](https://i.loli.net/2021/09/16/Dq75roLdIBnRj8t.png)  




![picture 15](https://i.loli.net/2021/09/16/Goxn5zrPi8kcyWH.png)  
