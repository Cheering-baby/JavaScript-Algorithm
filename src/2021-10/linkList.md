# 2021/10/25（实现一个链表）

设计链表的实现。您可以选择使用单链表或双链表。单链表中的节点应该具有两个属性：val 和 next。val 是当前节点的值，next 是指向下一个节点的指针/引用。如果要使用双向链表，则还需要一个属性 prev 以指示链表中的上一个节点。假设链表中的所有节点都是 0-index 的。

在链表类中实现这些功能：

- get(index)：获取链表中第 index 个节点的值。如果索引无效，则返回-1。
addAtHead(val)：在链表的第一个元素之前添加一个值为 val 的节点。插入后，新节点将成为链表的第一个节点。
- addAtTail(val)：将值为 val 的节点追加到链表的最后一个元素。
- addAtIndex(index,val)：在链表中的第 index 个节点之前添加值为 val  的节点。如果 index 等于链表的长度，则该节点将附加到链表的末尾。如果 index 大于链表长度，则不会插入节点。如果index小于0，则在头部插入节点。
- deleteAtIndex(index)：如果索引 index 有效，则删除链表中的第 index 个节点。

```jsx
var MyLinkedList = function () {
  this.head = null;
  this.size = 0;
  this.Node = function (val, next) {
    this.val = val;
    this.next = next;
    return { val: this.val, next: this.next };
  };
};

/**
 * @param {number} index
 * @return {number}
 */
MyLinkedList.prototype.get = function (index) {
  if (index < 0 || index >= this.size || this.head === null) return -1;
  let node = this.head;
  let i = 0;
  while (node.next && i < index) {
    node = node.next;
    i += 1;
  }

  return node.val;
};

/**
 * @param {number} val
 * @return {void}
 */
MyLinkedList.prototype.addAtHead = function (val) {
  if (this.head === null) {
    this.head = this.Node(val);
  } else {
    const node = this.Node(val, this.head);
    this.head = node;
  }
  this.size = this.size + 1;
};

/**
 * @param {number} val
 * @return {void}
 */
MyLinkedList.prototype.addAtTail = function (val) {
  if (this.head === null) {
    this.head = this.Node(val);
  } else {
    let i = 0;
    let node = this.head;
    while (node.next) {
      i = i + 1;
      node = node.next;
    }
    node.next = this.Node(val);
  }

  this.size = this.size + 1;
};

/**
 * @param {number} index
 * @param {number} val
 * @return {void}
 */
MyLinkedList.prototype.addAtIndex = function (index, val) {
  if (index > this.size) return null;
  if (index <= 0) {
    this.addAtHead(val);
  } else if (index === this.size) {
    this.addAtTail(val);
  } else {
    let i = 0;
    let prevNode = this.head;
    let nextNode;
    while (i < index - 1) {
      prevNode = prevNode.next;
      i++;
    }

    nextNode = prevNode.next;
    const node = this.Node(val, nextNode);
    prevNode.next = node;
    this.size = this.size + 1;
  }
};

/**
 * @param {number} index
 * @return {void}
 */
MyLinkedList.prototype.deleteAtIndex = function (index) {
  if (index < 0 || index >= this.size) return null;

  if (index === 0) {
    const next = this.head.next;
    this.head = next || null;
  } else {
    let prevNode = this.head;
    let i = 0;
    let nextNode;
    while (i < index - 1) {
      prevNode = prevNode.next;
      i++;
    }
    const curNode = prevNode.next;
    nextNode = curNode.next;
    prevNode.next = nextNode;
  }

  this.size = this.size - 1;
};

const showFn = () => {
  const arr = [];
  for (let i = 0; i < 12; i++) {
    if (obj.get(i) !== -1) {
      arr.push(obj.get(i));
    }
  }

  console.log(arr.join(" -> "));
};

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList* obj = new MyLinkedList();
 * int param_1 = obj->get(index);
 * obj->addAtHead(val);
 * obj->addAtTail(val);
 * obj->addAtIndex(index,val);
 * obj->deleteAtIndex(index);
 */

var obj = new MyLinkedList();
obj.addAtHead(7);
obj.addAtHead(2);
obj.addAtHead(1);
obj.addAtIndex(3, 0);
showFn();
```