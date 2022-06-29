# 双指针法

在[344.反转字符串 (opens new window)](https://programmercarl.com/0344.反转字符串.html)，我们使用双指针法实现了反转字符串的操作，**双指针法在数组，链表和字符串中很常用。**

接着在[字符串：替换空格 (opens new window)](https://programmercarl.com/剑指Offer05.替换空格.html)，同样还是使用双指针法在时间复杂度O(n)的情况下完成替换空格。

**其实很多数组填充类的问题，都可以先预先给数组扩容带填充后的大小，然后在从后向前进行操作。**

那么针对数组删除操作的问题，其实在[27. 移除元素 (opens new window)](https://programmercarl.com/0027.移除元素.html)中就已经提到了使用双指针法进行移除操作。

同样的道理在[151.翻转字符串里的单词 (opens new window)](https://programmercarl.com/0151.翻转字符串里的单词.html)中我们使用O(n)的时间复杂度，完成了删除冗余空格。

一些同学会使用for循环里调用库函数erase来移除元素，这其实是O(n^2)的操作，因为erase就是O(n)的操作，所以这也是典型的不知道库函数的时间复杂度，上来就用的案例了。

# [#](https://programmercarl.com/字符串总结.html#反转系列)反转系列

在反转上还可以在加一些玩法，其实考察的是对代码的掌控能力。

[541. 反转字符串II (opens new window)](https://programmercarl.com/0541.反转字符串II.html)中，一些同学可能为了处理逻辑：每隔2k个字符的前k的字符，写了一堆逻辑代码或者再搞一个计数器，来统计2k，再统计前k个字符。

其实**当需要固定规律一段一段去处理字符串的时候，要想想在在for循环的表达式上做做文章**。

只要让 i += (2 * k)，i 每次移动 2 * k 就可以了，然后判断是否需要有反转的区间。

因为要找的也就是每2 * k 区间的起点，这样写程序会高效很多。

在[151.翻转字符串里的单词 (opens new window)](https://programmercarl.com/0151.翻转字符串里的单词.html)中要求翻转字符串里的单词，这道题目可以说是综合考察了字符串的多种操作。是考察字符串的好题。

这道题目通过 **先整体反转再局部反转**，实现了反转字符串里的单词。

后来发现反转字符串还有一个牛逼的用处，就是达到左旋的效果。

在[字符串：反转个字符串还有这个用处？ (opens new window)](https://programmercarl.com/剑指Offer58-II.左旋转字符串.html)中，我们通过**先局部反转再整体反转**达到了左旋的效果。

# [#](https://programmercarl.com/字符串总结.html#kmp)KMP

KMP的主要思想是**当出现字符串不匹配时，可以知道一部分之前已经匹配的文本内容，可以利用这些信息避免从头再去做匹配了。**

KMP的精髓所在就是前缀表，在[KMP精讲 (opens new window)](https://programmercarl.com/0028.实现strStr.html)中提到了，什么是KMP，什么是前缀表，以及为什么要用前缀表。

前缀表：起始位置到下标i之前（包括i）的子串中，有多大长度的相同前缀后缀。

那么使用KMP可以解决两类经典问题：

1. 匹配问题：[28. 实现 strStr()(opens new window)](https://programmercarl.com/0028.实现strStr.html)
2. 重复子串问题：[459.重复的子字符串(opens new window)](https://programmercarl.com/0459.重复的子字符串.html)

再一次强调了什么是前缀，什么是后缀，什么又是最长相等前后缀。

前缀：指不包含最后一个字符的所有以第一个字符开头的连续子串。

后缀：指不包含第一个字符的所有以最后一个字符结尾的连续子串。

然后**针对前缀表到底要不要减一，这其实是不同KMP实现的方式**，我们在[KMP精讲 (opens new window)](https://programmercarl.com/0028.实现strStr.html)中针对之前两个问题，分别给出了两个不同版本的的KMP实现。

其中主要**理解j=next[x]这一步最为关键！**