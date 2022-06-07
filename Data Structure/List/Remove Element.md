# 203.Remove Linked List Elements

Given the `head` of a linked list and an integer `val`, remove all the nodes of the linked list that has `Node.val == val`, and return *the new head*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/06/removelinked-list.jpg)

```
Input: head = [1,2,6,3,4,5,6], val = 6
Output: [1,2,3,4,5]
```

**Example 2:**

```
Input: head = [], val = 1
Output: []
```

**Example 3:**

```java
Input: head = [7,7,7,7], val = 7
Output: []
```



## Solution 1: Sentinel Node

哨兵Node

因为只需要删除指定的val，因此只要到和val一样的node时将前序node的后指针.next指向val后面的node即可。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeElements(ListNode head, int val) {
			ListNode res = new ListNode(); //声明一个ListNode的对象
      res.next = head; //将res第一个位置指向head的头
      
      ListNode prev = res;  // 声明一个对象，它是res的头
      // 这个curr其实就是Sentinel Node
      ListNode curr = head.next;  // 声明一个对象，用于指向head.next
      
      while (curr != null) {  // 只要curr不为空，意味着head还有数字
        if (curr.next != val) prev.next = curr.next; //如果curr.next不相同，则放入res中
        else prev == curr; // 如果相同，不动位置
        curr = curr.next;  // curr往后移动一位
      }
      return res.next;
    }
}
```

