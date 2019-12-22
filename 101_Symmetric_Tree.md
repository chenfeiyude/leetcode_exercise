# Problem
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric:
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

But the following [1,2,2,null,3,null,3] is not:
```
    1
   / \
  2   2
   \   \
   3    3
```

# Solution 1. 2ms
Build a map contains each line's data, and then check each line is symmetric or not.

```
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
    public boolean isSymmetric(TreeNode root) {
        Map<Integer, List<Integer>> m = new HashMap<>();
        build(m, root, 0);
        if(!m.isEmpty()) {
            for(int i = 0; i < m.size(); i++) {
                List<Integer> vList = m.get(i);
                for(int j = 0; j < vList.size() / 2; j++) {
                if(vList.get(j) != vList.get(vList.size() - j - 1))
                    return false;
                }
            }
            
        }
        return true;
    }
    
    private void build(Map<Integer, List<Integer>> m, TreeNode root, int level) {
        
        if(root == null) {
            if(!m.containsKey(level))
                m.put(level, new ArrayList<>());
            m.get(level).add(null);
            return;
        }
        
        build(m, root.left, level + 1);
        if(!m.containsKey(level))
            m.put(level, new ArrayList<>());
        m.get(level).add(root.val);
        build(m, root.right, level + 1);
    }
}
```
