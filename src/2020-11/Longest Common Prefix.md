### 📖 文字题解
题目: 编写一个函数来查找字符串数组中的最长公共前缀。如果不存在公共前缀，返回空字符串 ""。

**思路一**: 横向比较，从第一个开始获取前后相同的最长公共前缀，如果中间遇到最长公共前缀为""的情况，可以退出循环，直接返回  
**复杂度**
+ 时间复杂度：O(mn)，m代表字符串的平均数量，n代表数组的长度
+ 空间复杂度：O(1)
```js
var longestCommonPrefix = function (strs) {
  function getCommonStr(str1, str2) {
    if(str1 === undefined || str2 === undefined) return "";
    let common = "";
    for (let i = 0; i < str1.length; i++) {
      if (str1[i] !== undefined && str1[i] === str2[i]) {
        common += str1[i];
      } else {
        break;
      }
    }
    return common;
  }
  if(!strs || strs.length === 0) return "";
  let commonStr = strs[0];
  for (let z = 1; z < strs.length; z++) {
    commonStr = getCommonStr(commonStr, strs[z]);
    if(commonStr.length === 0){
      break;
    }
  }
  return commonStr;
};
```
思路二: 纵向比较，以数组第一项为比较基准，循环数组第一项字段每一位和数组后面的字符的每一位作比较，没有遇到不同的继续比较，遇到不同就退出循环，得到结果  
**复杂度**
+ 时间复杂度：O(mn)，m代表字符串的平均数量，n代表数组的长度
+ 空间复杂度：O(1)
```js
var longestCommonPrefix = function (strs) {
  if(!strs || strs.length === 0) return "";
  let targetIndex;
  for(let i=0;i<strs[0].length;i++){
    if(targetIndex === undefined){
      for(let j=1;j<strs.length;j++){
        while(strs[j][i] !== strs[0][i]) {
          targetIndex = i;
          break;
        }
      }
    }
  }
  return strs[0].slice(0, targetIndex);
};
```
思路三: 二分查找，获取到数组长度最小的值，将最小长度的字符串进行二分拆解，进行比较



