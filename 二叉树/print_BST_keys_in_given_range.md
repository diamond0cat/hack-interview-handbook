

![picture 9](https://i.loli.net/2021/09/05/DOmfPbQw4M2xH8G.png)  


适当的剪支优化:

```java
public class Solution {
  public List<Integer> getRange(TreeNode root, int min, int max) {
    // Write your solution here.
    List<Integer> result =  new ArrayList<Integer>();
    getRange(root, min, max, result);
    return result;
  }
  
  public void getRange(TreeNode root, int min, int max, List<Integer> result) {
    if (root == null) {
      return;
    }
    if (root.key > min) {
      getRange(root.left, min, max, result);
    }
    if (root.key >= min && root.key <= max) {
      result.add(root.key);
    }
    if (root.key < max) {
      getRange(root.right, min, max, result);
    }
  }
}

```

时间复杂度： o(height) + O(# of nodes in the range)
SC=O(height)


