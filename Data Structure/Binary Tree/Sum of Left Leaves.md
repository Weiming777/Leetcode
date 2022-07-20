# 404.Sum of Left Leaves

Given the `root` of a binary tree, return *the sum of all left leaves.*

A **leaf** is a node with no children. A **left leaf** is a leaf that is the left child of another node.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/04/08/leftsum-tree.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: 24
Explanation: There are two left leaves in the binary tree, with values 9 and 15 respectively.
```

**Example 2:**

```
Input: root = [1]
Output: 0
```





## Solution 1: Iteration

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
    public int sumOfLeftLeaves(TreeNode root) {
        if (root == null) return 0;
        
        int res = 0;
        Queue<TreeNode> que = new LinkedList<>();
        que.offer(root);
        
        while (!que.isEmpty()) {
            int len = que.size();
            
            while(len > 0) {
                TreeNode node = que.poll();
                
                if (node.right != null) que.offer(node.right);
                if (node.left != null) que.offer(node.left);
                if (node.left != null && node.left.left == null && node.left.right == null) res += node.left.val;
                len--;
            }
        }
        
        return res;
    }
}
```





## Solution 2: Recursive

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
    public int sumOfLeftLeaves(TreeNode root) {
        if (root == null) return 0;
        int leftValue = sumOfLeftLeaves(root.left);
        int rightValue = sumOfLeftLeaves(root.right);
        
        int res = 0;
        
        if (root.left != null && root.left.left == null && root.left.right == null) {
            res += root.left.val;
        }
        
        return res + leftValue + rightValue;
    }
}
```

