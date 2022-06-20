# 面试题 02.07. 链表相交

给你两个单链表的头节点 headA 和 headB ，请你找出并返回两个单链表相交的起始节点。如果两个链表没有交点，返回 null 。

图示两个链表在节点 c1 开始相交：

![img](https://code-thinking-1253855093.file.myqcloud.com/pics/20211219221657.png)

题目数据 保证 整个链式结构中不存在环。

注意，函数返回结果后，链表必须 保持其原始结构 。

示例 1：

![img](https://code-thinking-1253855093.file.myqcloud.com/pics/20211219221723.png)

示例 2：

![img](https://code-thinking-1253855093.file.myqcloud.com/pics/20211219221749.png)

示例 3：

![img](https://code-thinking-1253855093.file.myqcloud.com/pics/20211219221812.png)![img](https://code-thinking-1253855093.file.myqcloud.com/pics/20211219221812.png)





## Solution :

先计算两个列表的长度，然后取最短的数值，求出长的与短的列表的差值，放置两个指针（长的指针肯定在中间，因为要保证指针后续长度和短列表长度相同，短列表指针在head上）。

开始比对两个指针是否相等，不相等共同往后移动一位，直至相等，结束。

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode curA = headA;
        ListNode curB = headB;
        int lenA = 0, lenB = 0;
        while (curA != null) { // 求链表A的长度
            lenA++;
            curA = curA.next;
        }
        while (curB != null) { // 求链表B的长度
            lenB++;
            curB = curB.next;
        }
        curA = headA;
        curB = headB;
        // 让curA为最长链表的头，lenA为其长度
        if (lenB > lenA) {
            //1. swap (lenA, lenB);
            int tmpLen = lenA;
            lenA = lenB;
            lenB = tmpLen;
            //2. swap (curA, curB);
            ListNode tmpNode = curA;
            curA = curB;
            curB = tmpNode;
        }
        // 求长度差
        int gap = lenA - lenB;
        // 让curA和curB在同一起点上（末尾位置对齐）
        while (gap-- > 0) {
            curA = curA.next;
        }
        // 遍历curA 和 curB，遇到相同则直接返回
        while (curA != null) {
            if (curA == curB) {
                return curA;
            }
            curA = curA.next;
            curB = curB.next;
        }
        return null;
    }
    
}
```

