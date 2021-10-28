# 2021/10/27（链表反转）

给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

## 示例

![https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

```
输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]
```

## 实现

### 解法一：原地反转

1→2→3→4→5可以理解为1←2←3←4←5

1. head的变化1→2→3→4→5，2→3→4→5，3→4→5，4→5，5，null
2. 用一个变量temp保存上次减少的部分，同时temp.next指向上一次temp，初始为null
3. 同时每一次result都保存temp

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
 * @return {ListNode}
 */
var reverseList = function(head) {
       if (head == null || head.next == null) {
            return head;
        }
        
        let temp = null;
        let result = null;
        while(head !== null) {
            temp = head;
            head = temp.next;
            temp.next = result;
            result = temp;
        }

        return result;
};
```

空间复杂度：O(1)

时间复杂度：O(N)

### 解法二：递归

```jsx
var reverseList = function(head) {
    if (head == null || head.next == null) return head
    const p = reverseList(head.next)
    head.next.next = head
    head.next = null
    return p
};
```