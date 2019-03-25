---
title: 克服JS的奇怪部分-型別與 JavaScript
date: 2017-10-20 00:00:00
tags: [javascript, js]
categories: [javascript]
top:
---
# 型別與 JavaScript

其他程式語言像是 Java，稱為「靜態型別」的方式處理，這代表必須在一開始就告知編譯器，你的變數是什麼資料型別，所以可能要有關鍵字，例如：bool，這變數型別是布林值`true or false`，不會是字串`"hello"`。
```java
// Static Typing
bool isNew = true;
bool isNew = "hello"; // an error
```
JavaScript是用「動態型別」的方式處理，
```javascript
// Dynamic Typing
var isNew = true;
isNew = 'string';
isNew = 1;
```

## 參考資源 (References)
* [JavaScript 全攻略：克服 JS 的奇怪部分](https://www.udemy.com/javascriptjs/learn/v4/overview)