# 142.Linked List Cycle II

Given the `head` of a linked list, return *the node where the cycle begins. If there is no cycle, return* `null`.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to (**0-indexed**). It is `-1` if there is no cycle. **Note that** `pos` **is not passed as a parameter**.

**Do not modify** the linked list.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

```
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

```
Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

**Example 3:**

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

```
Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.
```





## Solution: 

For solve this question, we need some mathematical trick.

If this list have a cycle, we can use two pointer, fast pointer and slow pointer. We can set if fast pointer is not equal with slow pointer, faster pointer move two steps and slower pointer move one step. In this case, faster pointer and slower pointer must have chance to meet each other in the cycle.

After that, we can mark the node  which faster pointer meet slower pointer, and set other two pointers called index1and index2. index1 is equal to head and index2 is equal to the node which faster and slower meet.

index1 and index2 one by one move one step and if they meet with each other, the node which they intersect is the begin node for this cycle.

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        
        while (fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                ListNode node_1 = head;
                ListNode node_2 = fast;
                
                while (node_1 != node_2) {
                    node_1 = node_1.next;
                    node_2 = node_2.next;
                }
                
                return node_1;
            }
        }
        
        return null;
    }
}
```

