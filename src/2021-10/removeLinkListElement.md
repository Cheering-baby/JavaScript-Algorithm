# 2021/10/28（移除链表元素）

给你一个链表的头节点 `head` 和一个整数 `val` ，请你删除链表中所有满足 `Node.val == val` 的节点，并返回 **新的头节点** 。

## 示例

### 示例1：

![https://assets.leetcode.com/uploads/2021/03/06/removelinked-list.jpg](https://assets.leetcode.com/uploads/2021/03/06/removelinked-list.jpg)

```jsx
输入：head = [1,2,6,3,4,5,6], val = 6
输出：[1,2,3,4,5]
```

### 示例2：

```jsx
输入：head = [], val = 1
输出：[]
```

### 示例3：

```jsx
输入：head = [7,7,7,7], val = 7
输出：[]
```

## 解法

### 解法1：遍历法

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
 * @param {number} val
 * @return {ListNode}
 */
var removeElements = function(head, val) {
 //生成一个头结点，为了避免head.val === val
 let virtualHead =  new ListNode(val + 1, head);

 let node = virtualHead;
 while(node.next) {
     if(node.next.val === val) {
         node.next = node.next.next;
     }else {
         node = node.next;
     }
 }

  return virtualHead.next;
};
```

### 解法2：递归

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
 * @param {number} val
 * @return {ListNode}
 */
var removeElements = function(head, val) {
  if(head === null) return head;
  let node = removeElements(head.next, val);
  if(head.val === val) {
     return node;
  } else {
     head.next = node;
     return head;
  }
};
```