---
title: 克服JS的奇怪部分-執行環境：程式執行
date: 2017-10-06 00:00:00
tags: [javascript, js]
categories: [javascript]
top:
---
# 執行環境：程式執行
JavaScript產生執行環境時，第一階段是創造，創造全域物件、`this`和外部環境與設定變數與函式到記憶體中，第二階端是執行，一行一行執行我們已經撰寫好的程式碼，進行編譯與轉換成電腦懂的語言。
```javascript
function b () {
  console.log('Called b!');
}
b(); // 返回: 'Called b!'
console.log(a); // 返回: undefined
var a = "Hello World!"
console.log(a); // 返回: "Hello World!"
```

## 參考資源 (References)
* [JavaScript 全攻略：克服 JS 的奇怪部分](https://www.udemy.com/javascriptjs/learn/v4/overview)