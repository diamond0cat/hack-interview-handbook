
```
In a binary search tree, find the node containing the largest number smaller than the given target number.

If there is no such number, return INT_MIN
```

```java
public int largestSmalelr(TreeNode root, int target) {
    int res = Integer.MIN_VALUE;

    while (root != null) {
        if (root.key >= target) {
            root = root.left;
        } else {
            res = root.key;
            root = root.right;
        }
    }
    return res;

}


```