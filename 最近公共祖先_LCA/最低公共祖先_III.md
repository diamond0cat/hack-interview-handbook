

```
Given two nodes in a binary tree, find their lowest common ancestor (the given two nodes are not guaranteed to be in the binary tree).

Return null If any of the nodes is not in the tree.

Assumptions

There is no parent pointer for the nodes in the binary tree

The given two nodes are not guaranteed to be in the binary tree

Examples

        5

      /   \

     9     12

   /  \      \

  2    3      14

The lowest common ancestor of 2 and 14 is 5

The lowest common ancestor of 2 and 9 is 9

The lowest common ancestor of 2 and 8 is null (8 is not in the tree)
```

```java
/**
 * public class TreeNode {
 *   public int key;
 *   public TreeNode left;
 *   public TreeNode right;
 *   public TreeNode(int key) {
 *     this.key = key;
 *   }
 * }
 */
public class Solution {
  public TreeNode lowestCommonAncestor(TreeNode root,
      TreeNode one, TreeNode two) {
          // corner case

          TreeNode lca = lca(root, one, two);
          if (lca == one) {
             if (lca(one, two,two) != null) return lca;
             else return null;
          } else if (lca == two) {
            if (lca(two, one, one) != null)return lca;
            else return null;
          }
          
          return lca;
  }
  private TreeNode lca(TreeNode root, TreeNode one, TreeNode two) {
    if (root == null) {
       return null;
     }
     if (root == one || root == two) {
       return root;
     }
     TreeNode left = lca(root.left, one, two);
     TreeNode right = lca(root.right, one, two);
     if (left != null && right != null) {
       return root;
     }
     return left != null ? left : right;
  }
}
```