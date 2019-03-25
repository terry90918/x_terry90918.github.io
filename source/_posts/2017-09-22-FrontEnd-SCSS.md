---
title: 前端工程師手冊-SCSS
date: 2017-09-22 17:08:25
tags: [css, scss]
categories: [scss]
top:
---
# SCSS 

## 簡介
`SCSS`是`Sass`延伸出來更接近`CSS3`的前置處理語言，讓開發者可以撰寫簡潔、富語意、重複性佳、可維護性佳和可延展性佳的程式碼。

## 特色

### 變數
使用`($)`設定變數，用冒號`(:)`來指定變數的值。變數可以再進行作加減乘除餘`(`+-*/%`)`運算，最特別的是字串與顏色色碼也可以進行運算。

> 對於會套用到整個網站的每個顏色、字體建議都先定義成變數
> 要使用像 red、blue 的英文字詞來指定顏色，而是要用16進位碼來定義，例如 red 應該寫成 #ff0000
> 在 CSS 類別中定義時，按照英文字元 A-Za-z 來排列其中的 CSS 樣式定義

```SCSS
/* SCSS */
$w: 200px;
$h: 100px;
.example {
  width: $w;
  height: $h * 2;
}
```

轉譯後
```CSS
/* CSS */
.example {
  width: 200px;
  height: 200px;
}
```

### 巢狀結構
可以清楚明瞭的知道階層定義，父元素與子元素關係。符號`(&)`來定義，代表是黏在一起中間沒有空格。

```SCSS
/* SCSS */
$w: 200px;
$h: 100px;
$m: 5px;
$p: 10px;
ul {
  margin: $m;
  li {
    padding: $p;
    &.example {
      width: $w;
      height: $h;
    }
  }
}
```

轉譯後
```CSS
/* CSS */
ul {
  margin: 5px;
}
ul li {
  padding: 10px;
}
ul li.example {
  width: 200px;
  height: 100px;
}
```

### @mixins
能幫記住`CSS`技巧，讓你不用再因回想原理而中斷思緒。

要記住的是`@minix`標記需要對應到`@include`標記。

> 整理屬於自己的 @mixins 集合，可讓開發事半功倍。

```SCSS
/* SCSS */
@mixin clearfix() {
  &:before,
  &:after {
    content: " ";
    display: table;
  }
  &:after {
    clear: both;
  }
}
.example {
  @include clearfix;
}
```

轉譯後
```CSS
/* CSS */
.example:before, .example:after {
  content: " ";
  display: table;
}
.example:after {
  clear: both;
}

```

帶參數與設定預設值，可以運算數字。

```SCSS
/* SCSS */
@mixin circle($size, $bgcolor) {
  border-radius: 50%;
  weight: $size;
  height: $size;
  font-size: $size / 3;
  background: $bgcolor;
}
.example {
  @include circle(30px, #fff);
}
```

轉譯後
```CSS
/* CSS */
.example {
  border-radius: 50%;
  weight: 30px;
  height: 30px;
  font-size: 10px;
  background: #fff;
}
```

### @extend 擴充/繼承
`@extend`是可以擴充原有的`CSS`，加上不同的定義或覆蓋原有的定義。
>建議：不要依賴繼承功能，當繼承次數變多，管理容易失去控制。

```SCSS
/* SCSS */
.red-color {
  color: red;
}
.example-1 {
  font-weight: bold;
  @extend .red-color;
}
.example-2 {
  @extend .red-color;
}
```

轉譯後
```CSS
/* CSS */
.red-color, .example-1, .example-2 {
  color: red;
}

.example-1 {
  font-weight: bold;
}
```

### @import 匯入
`@import` 可以引入許多的 **SCSS**，可將 SCSS 彙整成同一支檔案

( **_** ) 代表再編譯成 CSS 會忽略這些檔案，例如：`_alert.scss`

例如：要匯入`_alert.scss`，要注意的是只需要 `@import 'alert'`，不用加副檔名或下底線( **_** )，編譯程式會自動尋找對應的檔案

```SCSS
/* SCSS */
@import "mixins/alert";
@import "utilities/align";
@import "variables";
```

### @function 函式
`@function`可以定義自訂的函式，有程式語法，例如`@return、@if、@for、@each`等流程控制的特性及運算能力。 
[關於函式的更多資源](http://sass-lang.com/documentation/Sass/Script/Functions.html)
```SCSS
/* SCSS */
/* 範例一 @return */
@function calculate-width ($col-span) {
  @return 100% / $col-span;
}

.span-two {
  width: calculate-width(2); // spans 2 columns, width = 50%
}

.span-three {
  width: calculate-width(3); // spans 3 columns, width = 33.3%
}


/* 範例二 darken */
$awesome-blue: #2196f3;

a {
  background-color: $awesome-blue;
  padding: 10px 15px;
}

a:hover {
  background-color: darken($awesome-blue,10%);
}
```

## SCSS 優化之道

1. 設定常見變數(顏色、字體大小...等等)
1. improt 設計
1. 區隔 layout.scss，重複的 layout 整合
1. 斷點設計，sm 小、md 中、lg 大
1. page scss 獨立

## 綜合應用
* [SCSS 管理變數與模組](https://codepen.io/LovePanda/pen/JOyooW?editors=1100)
* [SCSS 迴圈與內容](https://codepen.io/LovePanda/pen/wPqawa)