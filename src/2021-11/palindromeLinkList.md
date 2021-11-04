# 2021/11/04（回文链表）

给定一个单链表的头结点`head`，请你判断是否为回文链表。如果是，返回`true`，否则返回`false`

示例1：

![https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg](https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg)

```
输入：head = [1,2,2,1]
输出：true
```

示例2：

![https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg](https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg)

```
输入：head = [1,2]
输出：false
```

解法一：

1. 设置快慢指针slow，fast和保持反转链表的reverse,slow每次走一次，fast每次走两步，循环每次都通过slow的指针反转前半部分的链表保存到reverse，直到fast走到最后，我们可以获得前半部分的反转链表和后半部分的链表
2. 通过比较这两部分的链表内容，获得结果

```jsx
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {boolean}
 */
var isPalindrome = function(head) {
    if(head.next === null) return true;

    let slow = head;
    let fast = head.next;
    let reverse = null;

    while(true) {
       let next = slow.next;
       slow.next = reverse;
       reverse = slow;
       slow = next;

       if(fast.next === null) {
         fast = slow;
         break;
       }
       fast = fast.next.next;

       if(fast === null) {
           fast = slow.next;
           break;
       }
    }
    
    while(reverse) {
        if(reverse.val !== fast.val) return false;
        
        reverse = reverse.next;
        fast = fast.next;
    }

    return true;
};
```