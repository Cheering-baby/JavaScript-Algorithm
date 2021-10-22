# 2021/10/21（三数之和）

给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有和为 0 且不重复的三元组。

注意：答案中不可以包含重复的三元组。

示例

```
输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]
```

- 遍历法：时间复杂度太高放弃

```js
var threeSum = function (nums) {
  // 遍历
  const arr = [];
  for (let i = 0; i < nums.length; i++) {
    const one = nums[i];

    for (let j = i + 1; j < nums.length; j++) {
      const two = nums[j];

      for (let z = j + 1; z < nums.length; z++) {
        const three = nums[z];

        if (one + two + three === 0) {
          if (
            !arr.find((x) => {
              const y = x.sort();
              const currentArr = [one, two, three].sort();
              return (
                y[0] === currentArr[0] &&
                y[1] === currentArr[1] &&
                y[2] === currentArr[2]
              );
            })
          )
            arr.push([one, two, three]);
        }
      }
    }
  }

  return arr;
};
```

- 排序加双指针
1. 特殊判断，对于数组长度n,当n小于3的时候返回空数组
2. 数组排序
3. 遍历排序后的数组 

      1. 当num[i]>0退出当前循环，后面都是大于0的数

      2. 重复元素，直接跳过

      3. 左指针设为L = i + 1，右指针设为R = n -1,当 L < R,执行循环

           1. 当nums[i] + nums[L] + nums[R] = 0,执行循环，判断左界和右界下一位置是否存在重复值，同时向下移动一位，寻求下个解

           2. 当三者之和大于0，说明nums[R]太大了，左移一位

           3. 当三者之和小于0，说明nums[L]太小了，右移一位

```js
var threeSum = function (nums) {
  // 遍历
  const arr = [];
  const n = nums.length;

  // 特殊判断
  if (n < 3) return [];

  //数组排序
  const sortArr = nums.sort(function (a, b) {
    return a - b;
  });
  // 遍历排序后的数组
  for (let i = 0; i < sortArr.length; i++) {
    // 当num[i]>0退出当前循环，后面都是大于0的数
    if (sortArr[i] > 0) continue;

    //重复元素，直接跳过
    if (i > 0 && sortArr[i] === sortArr[i - 1]) continue;

    // 左指针设为L = i + 1，右指针设为R = n -1,当 L < R,执行循环
    let L = i + 1;
    let R = n - 1;
    while (L < R) {
      const total = sortArr[i] + sortArr[L] + sortArr[R];
      if (total === 0) {
        arr.push([sortArr[i], sortArr[L], sortArr[R]]);
        L = L + 1;
        R = R - 1;
        // 当nums[i] + nums[L] + nums[R] = 0,执行循环，
        // 判断左界和右界下一位置是否存在重复值，同时向下移动一位，寻求下个解
        while (sortArr[L] === sortArr[L - 1]) {
          L = L + 1;
        }

        while (sortArr[R] === sortArr[R + 1]) {
          R = R - 1;
        }
      } else if (total > 0) {
        // 当三者之和大于0，说明nums[R]太大了，左移一位
        R = R - 1;
      } else if (total < 0) {
        // 当三者之和小于0，说明nums[L]太小了，右移一位
        L = L + 1;
      }
    }
  }

  return arr;
};
```