# 2021/11/19（两数相加）

给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

**示例 1：**

![https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2021/01/02/addtwonumber1.jpg](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2021/01/02/addtwonumber1.jpg)

```
输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[7,0,8]
解释：342 + 465 = 807.
```

**示例 2：**

```
输入：l1 = [0], l2 = [0]
输出：[0]
```

**示例 3：**

```
输入：l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
输出：[8,9,9,9,0,0,0,1]
```

**解法一：**

1. 生成一个新链表dummpNode，把这个值赋值给node，node负责不断生成next，carry代表的是下一个节点的进位，例如3+8 =11，carry置为1,2+5为7，carry置为0，下一次加会算上carry的进位
2. 当node1或者node2还存在值得情况继续循环，直到两个数都为null退出
3. 最后根据carry是否为1对最后一个加法是否需要进位
4. 返回dummpNext.next

```jsx
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
    var dummpNode = new ListNode();
    var node = dummpNode;
    var carry = 0;

    var node1 = l1;
    var node2 = l2;
    while(node1 || node2) {
        let addNumber = carry;
        if(node1) {
           addNumber += node1.val;
           node1 = node1.next;
        }
        if(node2) {
           addNumber += node2.val;
           node2 = node2.next;
        }
        if(addNumber >= 10) {
          carry = 1;
          node.next = new ListNode(addNumber - 10);
        } else {
          carry = 0;
          node.next = new ListNode(addNumber);
        }
        node = node.next;
    }

    if(carry === 1) {
        node.next = new ListNode(1)
    }

    return dummpNode.next;
};
```