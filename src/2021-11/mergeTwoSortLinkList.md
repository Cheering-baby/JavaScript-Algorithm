# 2021/11/16（合并两个有序列表）

将两个升序链表合并为一个新的 **升序** 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。

示例一：

![https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

```
输入：l1 = [1,2,4], l2 = [1,3,4]
输出：[1,1,2,3,4,4]
```

示例二：

```
输入：l1 = [], l2 = []
输出：[]
```

示例三：

```
输入：l1 = [], l2 = [0]
输出：[0]
```

解法一：

生成一个新的链表，设置指正i，j，分别从L1，L2的开头遍历，每次遍历都判断两个指针对应位置的val的大小，把新链表的next指向较小的val，较小的指针后移一位，知道其中一个指针结束，链表next指向另一个未结束的指针

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
var mergeTwoLists = function(l1, l2) {
   if(l1 === null) return l2;
   if(l2 === null) return l1;
   let node = new ListNode();
   let cur = node;
   let node1 = l1;
   let node2 = l2;
   while(node1 && node2) {
       if(node1?.val > node2?.val) {
           node.next = node2;
           node2 = node2.next;
       } else {
           node.next = node1;
           node1 = node1.next;
       }
       node = node.next;
   }

   if(node1) {
       node.next = node1;
   }else {
       node.next = node2;
   }

   return cur.next;
};
```

时间复杂度：O(n)

空间复杂度：O(n)

解法二：

选定一个头较小的链条作为i,另一条作为j，两个指针都从从头开始，每次拿j和i和.next做比较，如果值是两者中间插入i，i,j分别移动下下一个位置，如果j指针跑到最后则结束，中间如果遇到i.next为null则提前退出循环，这个时候把指针next指向剩余的指针j

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
var mergeTwoLists = function(l1, l2) {
   if(l1 === null) return l2;
   if(l2 === null) return l1;
   
   let i;
   let j;
   let target;
   if(l1.val <= l2.val) {
       i = l1;
       j = l2;
       target = l1;
   } else {
       i = l2;
       j = l1;
       target = l2;
   }
   
   while(j){
      if(i.next === null) break;
      if(i.val <= j.val && i.next.val > j.val) {
         let cur = i.next;
         let cur2 = j.next;
         i.next = j;
         j.next = cur;
         i = i.next;
         j = cur2;
      } else {
         i = i.next;
      }
   }

   if(j){
       i.next = j;
   }
   
   return target;
};
```

时间复杂度：O(n)

空间复杂度：O(1)