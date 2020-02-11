# Problem

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

Note: A leaf is a node with no children.

Example:

Given binary tree [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```
return its depth = 3.


# Solution 1. 0ms
go through each node with recursive method, and compare with max depth.

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    private int max = 0;
    public int maxDepth(TreeNode root) {
        currDepth(root, 0);
        return max;
    }
    
    private void currDepth(TreeNode root, int curr) {
        if(root == null)
            return;
        
        curr++;
        if(curr > max)
            max = curr;
        
        if(root.left != null)
            currDepth(root.left, curr);
        if(root.right != null)
            currDepth(root.right, curr);
    }
}
```
