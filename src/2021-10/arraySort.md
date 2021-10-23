# 2021/10/22（数组排序）

给你一个整数数组 `nums`，请你将该数组升序排列。

实例一：

```
输入：nums = [5,2,3,1]
输出：[1,2,3,5]
```

解法一：冒泡排序

1、循环数组，设置两个指针，x, y = x + 1

2、比较`nums[x]`和`nums[y]`的大小，`nums[x]` > `nums[y]`交换想`nums[x]`,`nums[y]`值的位置

```jsx
var sortArray = function (nums) {
  for (let x = 0; x < nums.length - 1; x++) {
    for (let y = x + 1; y < nums.length; y++) {
      if (nums[x] > nums[y]) {
        const particularValue = nums[x];
        nums[x] = nums[y];
        nums[y] = particularValue;
      }
    }
  }

  return nums;
};
```

时间复杂度：O($n^2$)

空间复杂度：O(1)

解法二：...

1. 从未排序的队列中分别选择最大值和最小值放在最右端和最左端，循环直到所有的数都排列结束
2. 定义L,R,分别最左端和最右端开始，从L到R比较出最大值和最小值，L和R分别加一，进行下一次循环，直到L>R,结束循环

```jsx
var sortArray = function (nums) {
  let L = 0;
  let R = nums.length - 1;
  
  while (L < R) {
    for (let i = L; i < R; i++) {
      const particularValue = nums[i];
      if (nums[i] < nums[L]) {
        nums[i] = nums[L];
        nums[L] = particularValue;
      } else if (nums[i] > nums[R]) {
        nums[i] = nums[R];
        nums[R] = particularValue;
      }
    }
    L = L + 1;
    R = R - 1;
  }

  return nums;
};
```

时间复杂度：O($n^2\over 2$)

空间复杂度：O(1)

第三种解法：选择排序

1. 以`nums[i]`为基准，从剩下未排序的选择最小的数的下标x,一次循环结束，x和i的下标位置对换，直到i到n（数组长度）-1退出循环

```jsx
var sortArray = function (nums) {
  const n = nums.length;
  let x;
  for (let i = 0; i < n - 1; i++) {
    x = i;
    for (let j = i + 1; j < n; j++) {
      if (nums[j] < nums[x]) {
        x = j;
      }
    }

    if (x !== undefined) {
      const particularValue = nums[i];
      nums[i] = nums[x];
      nums[x] = particularValue;
    }

    x = undefined;
  }

  return nums;
};
```

时间复杂度：O($n^2$)

空间复杂度：O(1)

第四种：插入排序

1. 从第一个开始，默认是一件被排序的序列
2. 取出下一个元素，和已经排序的序列从后向前扫描
3. 如果当前元素小于比较的元素，这个元素移动到下一位
4. 遇到大于的元素结束
5. 重复2-4，直到n-1

```jsx
var sortArray = function (nums) {
  const n = nums.length;
  for (let i = 1; i < n; i++) {
    let compareIndex = i;
    for (let j = i - 1; j >= 0; j--) {
      if (nums[compareIndex] < nums[j]) {
        const particularValue = nums[compareIndex];
        nums[compareIndex] = nums[j];
        nums[j] = particularValue;
        compareIndex = j;
      } else break;
    }
  }

  return nums;
};
```