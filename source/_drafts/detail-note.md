# 隨手筆記
## HTML
### label
當**label**元素包含**input**時候，可以點擊任何位置來觸發`input:checkbox`的**checked**。
```html
label
    input 
```
## CSS
### 選取器
#### [class^="className"]
以下舉例為選取所有包含**house**的**class name**。
```scss
[class^="house"]
```
## JavaScrit
### Native
#### Length 長度
`book.length;`
#### Push/Pop 推入/拿出
```javascript
var books = ["飢餓遊戲","星火燎原","自由幻夢"];
books.pop();
// "自由幻夢"
// books = ["飢餓遊戲","星火燎原"];
book.push("新書");
// 3
// books = ["飢餓遊戲","星火燎原","新書"];
```
#### Slice(開始,結束) 切割
```javascript
var numbers = [1,2,3,4,5];
number.slice(0,2);
// [1,2]
number.slice(-3,-2);
// [-3,-2];
number.slice(3);
// [4,5];
```
#### Reverse 反轉
```javascript
var numbers = [1,2,3,4,5];
numbers.reverse();
// [5, 4, 3, 2, 1]
```
#### Concat 接取
```javascript
var books1 = ["飢餓遊戲","星火燎原","自由幻夢"];
var books2 = ["魔戒現身","雙城奇謀","王者再臨"];
books1.concat(books2);
// ["飢餓遊戲", "星火燎原", "自由幻夢", "魔戒現身", "雙城奇謀", "王者再臨"]
```
#### [Fetch API](https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API/Using_Fetch)
```javascript
let myImage = document.querySelector('img');

fetch('flowers.jpg')
.then(function(response) {
    return response.blob();
})
.then(function(myBlob) {
    let objectURL = URL.createObjectURL(myBlob);
    myImage.src = objectURL;
});
```

### jQuery
#### append/prepend 末尾插入/開頭插入
```javascript
$("p").append("<b>Appended text</b>");
$("p").prepend("<b>Prepended text</b>");
```
