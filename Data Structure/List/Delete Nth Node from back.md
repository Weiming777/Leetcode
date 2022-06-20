# 19.Remove Nth Node From End of List

Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

```
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```

**Example 2:**

```
Input: head = [1], n = 1
Output: []
```

**Example 3:**

```
Input: head = [1,2], n = 1
Output: [1]
```

 

## Solution 1:

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        int length  = 0;
        ListNode first = head;
        while (first != null) {
            length++;
            first = first.next;
        }
        length -= n;
        first = dummy;
        while (length > 0) {
            length--;
            first = first.next;
        }
        first.next = first.next.next; // 不会越界么  Input：【1】 1 。 两个.next不就超出去了么
        return dummy.next;
    }
}
```





## Solution 2: three pointers

```java
class Solution {
  public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode dummy = new ListNode(-1);
    dummy.next = head;
    
    ListNode fast = dummy;
    ListNode slow = dummy;
    
    /*
    * 关键：
    * 因为是倒数第几个节点，所以提前让fast向前移动几个节点，这样才能保证后续当fast停下来的时候，slow指向正确的位置，也就是target		* 的位置
    */
    while (n-- > 0) {
      fast = fast.next;
    }
    
    ListNode prev = null;
    
    while (fast != null) {
      prev = slow;
      slow = slow.next;
      fast = fast.next;
    }
    
    prev.next = slow.next;
    
    return dummy.next; //因为一直在dummy上操作，而dummy第二位就是head，所以dummy.next
    
  }
}
```

