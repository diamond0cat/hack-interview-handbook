


https://www.geeksforgeeks.org/find-all-possible-trees-with-given-inorder-traversal/
```

Given an array that represents Inorder Traversal, find all possible Binary Trees with the given Inorder traversal and print their preorder traversals.
Examples: 
 

Input:   in[] = {3, 2};
Output:  Preorder traversals of different possible Binary Trees are:
         3 2
         2 3
Below are different possible binary trees
    3        2
     \      /
      2    3

Input:   in[] = {4, 5, 7};
Output:  Preorder traversals of different possible Binary Trees are:
          4 5 7 
          4 7 5 
          5 4 7 
          7 4 5 
          7 5 4 
Below are different possible binary trees
  4         4           5         7       7
   \          \       /   \      /       /
    5          7     4     7    4       5
     \        /                  \     /
      7      5                    5   4 


```
1) Initialize list of Binary Trees as empty.  
2) For every element in[i] where i varies from 0 to n-1,
    do following
......a)  Create a new node with key as 'arr[i]', 
          let this node be 'node'
......b)  Recursively construct list of all left subtrees.
......c)  Recursively construct list of all right subtrees.
3) Iterate for all left subtrees
   a) For current leftsubtree, iterate for all right subtrees
        Add current left and right subtrees to 'node' and add
        'node' to list.
```


```java
package com.laioffer.tree;
import java.util.*;

class Node {
    int val;
    Node left, right;
    public Node(int val) {
        this.val = val;
        left = null;
        right = null;
    }
}
public class BinaryTree {
    Node root;
    void preOrder(Node node) {
        if (node != null) {
            System.out.print(node.val + "  ");
            preOrder(node.left);
            preOrder(node.right);
        }
    }

    //construct all possible trees with given inorder traversal stores in an array from arr[start] to arr[end]
    List<Node> getTrees(int[] arr, int start, int end) {
        // List to store all possible trees
        List<Node> trees = new ArrayList<>();

        // base case
        // if start > end then subtree will be empty so returning NULL in the list
        if (start > end) {
            trees.add(null);
            return trees;
        }
        // iterating through all values from start to end from constructing left and right subtree recursively
        for (int i = start; i <= end; i++) {
            // build left subtree
            List<Node> ltrees = getTrees(arr, start, i - 1);

            // build right subtree
            List<Node> rtrees = getTrees(arr, i + 1, end);

            // loop through all left and right subtrees and connecting them to ith root
            for (int j = 0; j < ltrees.size(); j++) {
                for (int k = 0; k < rtrees.size(); k++) {

                    // arr[i] is root
                    Node node = new Node(arr[i]);

                    node.left = ltrees.get(j);
                    node.right = rtrees.get(k);

                    trees.add(node);
                }
            }
        }
        return trees;
    }


    public static void main(String args[]) {
        int in[] = {1, 2, 3};
        int n = in.length;
        BinaryTree tree = new BinaryTree();
        List<Node> trees = tree.getTrees(in, 0, n - 1);
        System.out.println("Preorder traversal of different "+
                " binary trees are:");
        for (int i = 0; i < trees.size(); i++) {
            tree.preOrder(trees.get(i));
            System.out.println("");
        }
    }
}   
 ```