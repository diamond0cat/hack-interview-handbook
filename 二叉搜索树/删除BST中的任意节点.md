

1. 只有左孩子
2. 只有右孩子
3. 自己就是叶子， 可以理解成1或2的特殊情况，甚至不需要单独拿出来处理
4. 既有左子树又有右子树， 这是最难的case --> Hibbard deletion

找到s = min(d.right)

s是d的后继节点：

```java
s.right = deleteMin(d.right); //把s从原来的位置删除，把d.right挂接到s.right
s.left = d.left;  //d.left挂接到s.left
```



```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode deleteNode(TreeNode root, int key) {
        // sanity check
        if (root == null) return root;
  
        if (root.val == key) {
            //只有右子树没有左子树,这里既没有左子树也没有右子树的情况被一起处理了
            if (root.left == null) return root.right;
            if (root.right == null) return root.left;
            if (root.right.left == null) {
                root.right.left = root.left;
                return root.right;
            }
            // with left and right
            TreeNode newRoot = deleteSmallest(root.right);
            newRoot.left = root.left;
            newRoot.right = root.right;
            return newRoot;
        }
        if (root.val < key) {
            root.right = deleteNode(root.right, key);
        } else if (root.val > key) {
            root.left = deleteNode(root.left, key);
        }
        return root;  
    }
    //把smallest从right subtree删除并返回smallest
    private TreeNode deleteSmallest(TreeNode root) {
        while (root.left.left != null) {  //一路向左
            root = root.left;
        }
        TreeNode smallest = root.left;
        root.left = root.left.right;
        return smallest;
    }
}
```
