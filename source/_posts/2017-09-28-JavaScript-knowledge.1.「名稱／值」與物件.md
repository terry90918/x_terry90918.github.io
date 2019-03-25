---
title: 克服JS的奇怪部分-「名稱／值」與物件
date: 2017-09-28 00:00:00
tags: [javascript, js]
categories: [javascript]
top:
---

# 「名稱／值」
執行環境中一個名稱只會有一個值，而值可以是更多的名稱與值。  
例如：City 是名稱，Taipei 是值。`City = "Taipei"`

# 物件
JavaScript的物件就是**(名稱/值)**的組合，而這個值又可以是另一個物件**(名稱/值)**。
```
Name/
  Name/
    Name/Value
    Name/Value
    Name/Value
  Name/
    Name/Value
    Name/Value
    Name/Value
Address: {
  Street: 'Zhongxiao East Road'
  Number: 100
  Apartment: {
    Fllor: 3,
    Number: 301
  }
}
```
|名稱|值|
|--|--|
|Address|Street,Number,Apartment|
|Street|'Zhongxiao East Road'|
|Number|100|
|Apartment|Fllor,Number|
|Fllor|3|
|Number|301|

## 參考資源 (References)
* [JavaScript 全攻略：克服 JS 的奇怪部分](https://www.udemy.com/javascriptjs/learn/v4/overview)