---
title: 克服JS的奇怪部分範圍、ES6與let
date: 2017-10-16 00:00:00
tags: [javascript, js]
categories: [javascript]
top:
---
# 範圍、ES6 與 let
`let`讓JavaScript引擎使用一種東西叫「區塊範圍」（block scoping），它會被創造在執行階段，變數仍然會被放入記憶體中並設為`undefined`，它只會在區塊中被宣告，區塊通常被定義在大括號中，當被宣告在裡面時只能在裡面被取用，所以當有一個程式於迴圈重複啟用時，使用`let`每次進行迴圈，變數在記憶體中都是不同的，這就是「區塊範圍」。
```javascript
var a = 2;
var b = 1
if (a > b) {
  let c = true;
  console.log(c);
  // 返回: true
}
console.log(c);
// 返回: Uncaught ReferenceError: c is not defined
```

## 參考資源 (References)
* [JavaScript 全攻略：克服 JS 的奇怪部分](https://www.udemy.com/javascriptjs/learn/v4/overview)