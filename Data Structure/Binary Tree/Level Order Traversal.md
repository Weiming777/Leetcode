# 102.Binary Tree Level Order Traversal

Given the `root` of a binary tree, return *the level order traversal of its nodes' values*. (i.e., from left to right, level by level).

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
```

**Example 2:**

```
Input: root = [1]
Output: [[1]]
```

**Example 3:**

```
Input: root = []
Output: []
```





## Solution 1: Iteration  BFS（Breath First Search）广度优先搜索

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
      	iteration(root, result);
      	return result;
    }
  
  	public void iteration (TreeNode root, List<List<Integer>> result) {
      if (root == null) {
        return;
      }
      
      Queue<TreeNode> que = new Linkedlist<>();
      que.offer(root);
      
      while (!que.isEmpty()) {
        List<Integer> list = new ArrayList<>();
        int len = que.size();
        
        while (len > 0) {
          TreeNode temp = que.pop();
          list.add(temp.val);
          
          if (temp.left != null) que.offer(temp.left);
          if (temp.right != null) que.offer(temp.right);
          len--;
        }
        result.add(list);
      }
    }
    
}
```





## Solution 2: Recursion  DFS

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
    public List<List<Integer>> resList = new ArrayList<List<Integer>>();

    public List<List<Integer>> levelOrder(TreeNode root) {
        checkFun01(root,0);

        return resList;
    }

    //DFS--递归方式
    public void checkFun01(TreeNode node, Integer deep) {
        if (node == null) return;
        deep++;

        if (resList.size() < deep) {
            //当层级增加时，list的Item也增加，利用list的索引值进行层级界定
            List<Integer> item = new ArrayList<Integer>();
            resList.add(item);
        }
        resList.get(deep - 1).add(node.val);

        checkFun01(node.left, deep);
        checkFun01(node.right, deep);
    }
}
```





# 107.Binary Tree Level Order Traversal II

Given the `root` of a binary tree, return *the bottom-up level order traversal of its nodes' values*. (i.e., from left to right, level by level from leaf to root).

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[15,7],[9,20],[3]]
```

**Example 2:**

```
Input: root = [1]
Output: [[1]]
```

**Example 3:**

```
Input: root = []
Output: []
```





## Solution 1: Iteration   BFS

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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        iteration(root, result);
        return result;
    }
    
    public void iteration (TreeNode root, List<List<Integer>> result) {
        if (root == null) return;
        Queue<TreeNode> que = new LinkedList<>();
        que.offer(root);
        
        while (!que.isEmpty()) {
            List<Integer> list = new ArrayList<>();
            int len = que.size();
            
            while (len > 0) {
                TreeNode temp = que.poll();
                list.add(temp.val);
                
                if (temp.left != null) que.add(temp.left);
                if (temp.right != null) que.add(temp.right);
                len--;
            }
            result.add(0,list);
        }
    }
}

```





## Solution 2: Recursion      DFS

```java
class Solution {
    List<List<Integer>> levels = new ArrayList<List<Integer>>();

    public void helper(TreeNode node, int level) {
        // start the current level
        if (levels.size() == level)
            levels.add(new ArrayList<Integer>());

         // append the current node value
         levels.get(level).add(node.val);

         // process child nodes for the next level
         if (node.left != null)
            helper(node.left, level + 1);
         if (node.right != null)
            helper(node.right, level + 1);
    }
    
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        if (root == null) return levels;
        helper(root, 0);
        Collections.reverse(levels);
        return levels;
    }
}
```





# 199.Binary Tree Right Side View

Given the `root` of a binary tree, imagine yourself standing on the **right side** of it, return *the values of the nodes you can see ordered from top to bottom*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/14/tree.jpg)

```
Input: root = [1,2,3,null,5,null,4]
Output: [1,3,4]
```

**Example 2:**

```
Input: root = [1,null,3]
Output: [1,3]
```

**Example 3:**

```
Input: root = []
Output: []
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
public List<Integer> rightSideView(TreeNode root) {
    	List<Integer> list = new ArrayList<>();
  		Deque<TreeNode> deque = new LinkedList<>();
  		
  		if (root == null) {
				return list;
      }
  
  		deque.offerLast(root);
  		while (!deque.isEmpty) {
        int levelSize = deque.size();
        
        for (int i = 0; i < levelSize; i++) {
          TreeNode node = deque.pollFirst();
          
          if (node.left != null) {
            deque.addFisrt(node.left);
          }
          if (node.right != null) {
            deque.addFirst(node.right);
          }
          if (i == levelSize - 1) {
            list.add(node.val);
          }
        }
      }
  		return list;
    }
}
```









# 637.Average of Levels in Binary Tree

Given the `root` of a binary tree, return *the average value of the nodes on each level in the form of an array*. Answers within `10-5` of the actual answer will be accepted.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/09/avg1-tree.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [3.00000,14.50000,11.00000]
Explanation: The average value of nodes on level 0 is 3, on level 1 is 14.5, and on level 2 is 11.
Hence return [3, 14.5, 11].
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/03/09/avg2-tree.jpg)

```
Input: root = [3,9,20,15,7]
Output: [3.00000,14.50000,11.00000]
```







## Solution 1: Iteration  BFS

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
    public List<Double> averageOfLevels(TreeNode root) {
        List<Double> list = new ArrayList<>();
        
        if (root == null) {
            return list;
        }
        
        Queue<TreeNode> que = new LinkedList<>();
        
        que.offer(root);
        while (!que.isEmpty()) {
            double sum = 0.0;
            int len = que.size();
            int nums = que.size();
            while (len > 0) {
                TreeNode temp = que.poll();
                sum += temp.val;
                if (temp.left != null) {
                    que.offer(temp.left);
                }
                if (temp.right != null) {
                    que.offer(temp.right);
                }
                len--;
            }
            list.add(sum/nums);
        }
        return list;
    }
}
```







# 429.N-ary Tree Level Order Traversal

Given an n-ary tree, return the *level order* traversal of its nodes' values.

*Nary-Tree input serialization is represented in their level order traversal, each group of children is separated by the null value (See examples).*

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/10/12/narytreeexample.png)

```
Input: root = [1,null,3,2,4,null,5,6]
Output: [[1],[3,2,4],[5,6]]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2019/11/08/sample_4_964.png)

```
Input: root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
Output: [[1],[2,3,4,5],[6,7,8,9,10],[11,12,13],[14]]
```





## Solution 1: BSF Iteration

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (root == null) return res;
        Queue<Node> que = new ArrayList<>();
      
      	que.offer(root);
      
      	while (!que.isEmpty()) {
          int size = que.size();
          List<Integer> list = new ArrayList<>();
          for (int i = 0; i < size; i++) {
            Node cur = que.poll();
            list.add(cur.val);
            for (Node children : cur.children) {
              que.offer(children);
            }
          }
        }
    }
}
```





```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (root == null) return res;
        Queue<Node> que = new LinkedList<>();
      
      	que.offer(root);
      
      	while (!que.isEmpty()) {
          int size = que.size();
          List<Integer> list = new ArrayList<>();
          for (int i = 0; i < size; i++) {
            Node cur = que.poll();
            list.add(cur.val);
            for (Node children : cur.children) {
              que.offer(children);
            }
            
          }
        
           res.add(list);
        }
        
        return res;
    }
}
```





## Solution 2: Recursion  DFS

```java
class Solution {

    private List<List<Integer>> result = new ArrayList<>();

    public List<List<Integer>> levelOrder(Node root) {
        if (root != null) traverseNode(root, 0);
        return result;
    }

    private void traverseNode(Node node, int level) {
        if (result.size() <= level) {
            result.add(new ArrayList<>());
        }
        result.get(level).add(node.val);
        for (Node child : node.children) {
            traverseNode(child, level + 1);
        }
    }
}
```







# 515.Find Largest Value in Each Tree Row

Given the `root` of a binary tree, return *an array of the largest value in each row* of the tree **(0-indexed)**.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/08/21/largest_e1.jpg)

```
Input: root = [1,3,2,5,3,null,9]
Output: [1,3,9]
```

**Example 2:**

```
Input: root = [1,2,3]
Output: [1,3]
```





## Solution : BFS Iteration

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
    public List<Integer> largestValues(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) return res;
        
        Queue<TreeNode> que = new LinkedList<>();
        que.offer(root);
        
        while (!que.isEmpty()) {
            int size = que.size();
            int maxVal = Integer.MIN_VALUE;
            for (int i = 0; i < size; i++) {
                TreeNode node = que.poll();
                maxVal = Math.max(maxVal, node.val);
                
                if (node.left != null) que.offer(node.left);
                if (node.right != null) que.offer(node.right);
                
            }
            res.add(maxVal);
        }
        return res;
    }
}
```







# 116.Populating Next Right Pointers in Each Node

You are given a **perfect binary tree** where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2019/02/14/116_sample.png)

```
Input: root = [1,2,3,4,5,6,7]
Output: [1,#,2,3,#,4,5,6,7,#]
Explanation: Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```

**Example 2:**

```
Input: root = []
Output: []
```





## Solution 1: BFS

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node next;

    public Node() {}
    
    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, Node _left, Node _right, Node _next) {
        val = _val;
        left = _left;
        right = _right;
        next = _next;
    }
};
*/

class Solution {
    public Node connect(Node root) {
        if (root == null)  return root;
        Queue<Node> que = new LinkedList<>();
        que.offer(root);
        
        while (!que.isEmpty()) {
            int size = que.size();
            
            Node cur = que.poll();
            
            if (cur.left != null) que.offer(cur.left);
            if (cur.right != null) que.offer(cur.right);
            
            for (int index = 1; index < size; index++) {
                Node next = que.poll();
                            
                if (next.left != null) que.offer(next.left);
                if (next.right != null) que.offer(next.right);
                
                cur.next = next;
                cur = next;
            }
            
        }
        
        return root;
    }
}
```





## Solution 2: DFS

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node next;

    public Node() {}
    
    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, Node _left, Node _right, Node _next) {
        val = _val;
        left = _left;
        right = _right;
        next = _next;
    }
};
*/

class Solution {
    public Node connect(Node root) {
        if (root == null) return null;
        
        if (root.left != null) {
            root.left.next = root.right;
        }
        if (root.right != null && root.next != null) {
            root.right.next = root.next.left;
        }
        
        root.left = connect(root.left);
        root.right = connect(root.right);
        
        return root;
    }
}
```