recursion:

```java
    public TreeNode searchBST(TreeNode root, int val) {
        // Write your code here.
        if (root == null) return null;
        if (root.val == val) return root;

        if (root.val < val) {
            return searchBST(root.right, val);
        } else {
            return searchBST(root.left, val);
        }
    }
```


iterative:

```java
    public TreeNode searchBST(TreeNode root, int val) {
        // Write your code here.
        while (root != null) {
            if (root.val == val) return root;

            if (root.val < val) {
                root = root.right;
            } else {
                root = root.left;
            }
        }
        return null;
    }
```