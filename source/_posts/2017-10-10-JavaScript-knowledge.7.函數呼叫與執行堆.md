---
title: 克服JS的奇怪部分-函數呼叫與執行堆
date: 2017-10-10 00:00:00
tags: [javascript, js]
categories: [javascript]
top:
---
# 函數呼叫與執行堆
```javascript
function a() { b(); }
function b() { console.log('Called b!'); }
a();
```
名稱與括號是呼叫函數`a()`，執行堆是JavaScript一次只執行一件事順序，剛開始是全域執行環境，接著呼叫了`a();`，`a()`執行時發現呼叫`b()`，會在執行推的順位上先執行`b()`，直到`b()`執行完畢移出執行推，才會繼續執行下一層尚未執行完畢的`a()`。

* 執行啟用順序 ↓
  1. 全域執行環境
  1. `a();`
  1. `b();`

* 執行堆疊順序 ↓
  1. `b();`
  1. `a();`
  1. 全域執行環境

## 參考資源 (References)
* [JavaScript 全攻略：克服 JS 的奇怪部分](https://www.udemy.com/javascriptjs/learn/v4/overview)