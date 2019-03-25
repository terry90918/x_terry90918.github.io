---
title: 克服JS的奇怪部分-執行環境：創造與提升
date: 2017-10-02 00:00:00
tags: [javascript, js]
categories: [javascript]
top:
---
# 執行環境：創造與提升
當宣告變數與函示時，它們會被提升，變數不會給等號後面的值，直到JavaScript逐行執行到代碼的宣告位置，才會設定值，函式則是全部先被執行。  
全域環境在被創造時，有「全域變數」、「`this`」與「外部環境」在記憶體中，全域變數只會在全域環境，而`this`會永遠在執行環境，接著才會執行我們所撰寫的程式碼，它會知道你在哪裡創造變數與函式，並設定記憶體空間給變數與函式，這就是提升。但這不是將變數與函式拉到最前面，這表示在逐行程式碼之前，JavaScript已為變數與函式存入記憶體中，建立空間了。
```javascript
b(); // 'Called b!'
console.log(a); // undefined

var a = "Hello World!"
function b () {
  console.log('Called b!');
}
```

## 參考資源 (References)
* [JavaScript 全攻略：克服 JS 的奇怪部分](https://www.udemy.com/javascriptjs/learn/v4/overview)