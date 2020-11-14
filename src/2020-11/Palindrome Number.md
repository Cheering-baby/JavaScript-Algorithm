### 📖 文字题解
题目: 判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

**思路一**: 通过将数字转化成字符串的方式比较反转前的字符串比较
**复杂度**
+ 时间复杂度：O(n)
+ 空间复杂度：O(1)
```js
//ES6
var isPalindrome = function(obj){
    const objStr = obj.toString();
    return objStr.split('').reverse().join('') === objStr;
}
//ES5
var isPalindrome = function(obj){
    var str = '';
    var objStr = obj.toString();
    var len = objStr.length;
    for(var i = len - 1;i >= 0;i--){
        str += objStr[i];
    }
    return str === objStr;
}
```
思路二: 不通过字符串比较的方式，通过反转数字本身，只需要反转后半部分的内容和前半部分的内容进行比较，首先处理一些临界情况，所有的负数和结尾为0的数都不可能是回文数。
**复杂度**
+ 时间复杂度：O(logn)
+ 空间复杂度：O(1)
```js
var isPalindrome = function(obj){
  if(obj < 0 || (obj % 10 === 0 && obj !== 0)){
      return false;
  }
  var revertedNumber = 0;
  while(obj > revertedNumber) {
     revertedNumber = revertedNumber * 10 + obj % 10;
     obj = Math.floor(obj / 10);
  }
  // 当数字长度为奇数时，我们可以通过 revertedNumber/10 去除处于中位的数字。
  // 例如，当输入为 12321 时，在 while 循环的末尾我们可以得到 x = 12，revertedNumber = 123，
  // 由于处于中位的数字不影响回文（它总是与自己相等），所以我们可以简单地将其去除。
  return obj === revertedNumber || obj === Math.floor(revertedNumber / 10);
}
```



