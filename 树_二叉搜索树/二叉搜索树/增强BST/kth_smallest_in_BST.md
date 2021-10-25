- 怎么优化？

![picture 7](https://i.loli.net/2021/10/26/NkDmwWiVFI4rChA.png)  
--from the smallest element, do inorder traversal, until we meet the kth element


```java
Recursion:‌ ‌

    //‌ ‌return‌ ‌the‌ ‌kth‌ ‌smallest‌ ‌node‌ ‌in‌ ‌the‌ ‌current‌ ‌subtree‌ ‌of‌ ‌root.‌ ‌
    public‌ ‌TreeNode‌ ‌kth(TreeNode‌ ‌root,‌ ‌int‌ ‌k)‌ ‌{‌ ‌
        //‌ ‌base‌ ‌case‌ ‌
        if‌ ‌(root‌ ‌==‌ ‌null)‌ ‌return‌ ‌null;‌ ‌
        //‌ ‌induction‌ ‌rule‌ ‌
        if‌ ‌(root.numLeft‌ ‌==‌ ‌k‌ ‌-‌ ‌1)‌ ‌{‌ ‌
            return‌ ‌root;‌ ‌
        }‌ ‌else‌ ‌if‌ ‌(root.numLeft‌ ‌>=‌ ‌k)‌ ‌{‌ ‌
            return‌ ‌kth(root.left,‌ ‌k);‌ ‌
        }‌ ‌else‌ ‌{‌ ‌
            return‌ ‌kth(root.right,‌ ‌k‌ ‌-‌ ‌root.numLeft‌ ‌-‌ ‌1);‌ ‌
        }‌ ‌
    }‌ ‌
 ‌
tail‌ ‌recursion‌ ‌→‌ ‌iterative‌ ‌solution‌ ‌
Iterative:‌ ‌

    public‌ ‌TreeNode‌ ‌kth(TreeNode‌ ‌root,‌ ‌int‌ ‌k)‌ ‌{‌ ‌
        while‌ ‌(root‌ ‌!=‌ ‌null)‌ ‌{‌ ‌
            if‌ ‌(root.numLeft‌ ‌==‌ ‌k‌ ‌-‌ ‌1)‌ ‌{‌ ‌
                return‌ ‌root;‌ ‌
            }‌ ‌ ‌
            if‌ ‌(root.numLeft‌ ‌>=‌ ‌k)‌ ‌{‌ ‌
                root‌ ‌=‌ ‌root.left;‌ ‌
            }‌ ‌else‌ ‌{‌ ‌
                k‌ ‌=‌ ‌k‌ ‌-‌ ‌root.numLeft‌ ‌-‌ ‌1;‌ ‌
                root‌ ‌=‌ ‌root.right;‌ ‌
            }‌ ‌
        }‌ ‌
        return‌ ‌null;‌ ‌
    }‌ ‌


Time:‌ ‌O(logn)‌ 
```