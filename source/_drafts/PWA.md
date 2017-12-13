---
title: Progressive Web Apps
date: 2017-11-10 10:00:00
tags: [PWA]
categories: [PWA]
permalink:
thumbnail:
top:
---
# Progressive Web Apps

Google I/O 2017 Web App，一種新的方式在網絡上提供驚人的用戶體驗。涵蓋使用者體驗的範圍，包括
* Reliable - 在不確定的網絡條件之下，加載瞬間永不顯示離線恐龍。
* Fast - 快速響應用戶與柔滑平滑動畫交互的動作，無需滾動。
* Engaging - 感覺像設備上的原生應用程序，身臨其境的用戶體驗。

這種新的質量水平允許應用程序在用戶的主屏幕上獲得一個地方。

---

## Reliable

當從用戶的主屏幕啟動，使應用程序能夠即時加載，不管網絡狀態如何。
工程師用 JavaScript 編寫，就像是一個客戶端代理，並讓你在高速緩存中的控制以及如何對資源的請求作出回應。
通過預緩存關鍵資源就可以消除網絡上的依賴，確保為用戶提供即時可靠的體驗。
[Learn More](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers)

---

## Fast

如果加載時間超過 3 秒，53% 的用戶將放棄網站！
一旦加載，用戶期望他們是快速的 - 沒有 janky 滾動或緩慢響應的界面。
[Learn More](https://developers.google.com/web/fundamentals/performance/)

---

## Engaging
逐行 Web 應用程序可以安裝在用戶的主屏幕上，無需應用程序商店。  
他們通過網絡應用程序清單文件提供身臨其境的全屏體驗，甚至可以通過網絡推送通知重新吸引用戶。  
Web 應用程序清單允許您控制應用程序的顯示方式及其啟動方式。  
您可以指定主屏幕圖標，啟動應用程序時加載的頁面，屏幕方向，甚至是否顯示瀏覽器 Chrome。  

[Web App Manifest](https://developers.google.com/web/fundamentals/engage-and-retain/web-app-manifest/)

[Web Push Notifications](https://developers.google.com/web/fundamentals/engage-and-retain/push-notifications/)

---

## 為什麼要建構 PWA ?
構建高質量的漸進式 Web 應用程序具有令人難以置信的優勢，使您可以輕鬆獲取用戶喜好，增加參與度並提高轉化次數。

[值得在主屏幕上。](https://developers.google.com/web/fundamentals/engage-and-retain/app-install-banners/)

當達到 Progressive Web App 標準時，Chrome 會提示用戶將 Progressive Web App 添加到主屏幕。

[無論網絡情況如何，可靠工作。](https://developers.google.com/web/showcase/2016/konga)

開發人員能夠發送少於63％的初始頁面加載數據，並減少 84% 的數據以完成第一筆交易！

[更多的參與](https://developers.google.com/web/showcase/2016/extra)

網頁推送通知，幫助多餘電子由 4X 提高參與度。
而這些用戶花費兩倍於網站上的時間。

[改進轉換率](https://developers.google.com/web/showcase/2016/aliexpress)

提供驚人的用戶體驗的能力幫助 AliExpress 將所有瀏覽器中的新用戶的轉化率提高了 104%，而 iOS 上的轉化率提高了 82%。

---

## Lighthouse
Lighthouse 是一種開源的自動化工具，用於提高 Progressive Web Apps 的質量，消除了以前需要的大量手動測試。 你甚至可以使用燈塔在持續集成系統，以捕捉退化。
[Learn More](https://developers.google.com/web/tools/lighthouse/)

---
## Service Worker
### Service Worker 介紹
Service Worker 是非常強大的 offline caching，讓使用者可以重複使用 cache，即時顯示畫面在網站或應用程式裡，提供優異的效能。

Service Worker 解決了 WEB 用戶無法離線瀏覽的問題，當網站處於離線狀態，沒有辦法利用網路得到更多資料之前，仍然可以提供基本體驗，讓網站更像 Native App、可以提供像是定期更新、推播通知等功能。

Service Workers 不能直接操作 DOM，但是可以通過 postMessage，把消息傳送給頁面，讓頁面去操作 DOM。

Service Worker，在瀏覽器的背景默默地執行，不需要透過網頁的操作觸發，Service Worker 有著自己的生命週期，為了使用 Service Worker，你的網站必須使用 Javascript 進行註冊，並且必須在 localhost 或 HTTPS 的環境底下，才能運行。

### Service Worker 步驟
1. Registering the Service Worker
    * 實作 Service Worker 之前，必須先註冊 Service Worker，才能夠執行 Service Worker 的生命週期
1. Setting up the Default Cache
    * 在 Service Worker 的 install 事件裡，設定預期 cache 路徑，儲存 App Shell 檔案
1. Clearing Old Cache
    * 一開始在 fetch 執行之前，會先觸發 activate 事件，我們可以在這個週期進行清除快取的動作，避免網站會一直存取舊的 cache 檔案
1. Handling Fetch Requests
    * 無論是儲存 App Shell 檔案或者是 API 內容，都需要透過 fetch 這個事件去處理攔截到的 Request 並回傳 Response，讓網站處於沒有網路時、仍然可以進行離線瀏覽。

---

### Simple Demo 1

簡單 Service Worker 運作，首先觀察以下 HTML 內容，透過 Javascript 註冊 Service Worker，設定 3 秒後，顯示一張『狗狗』圖片。

```html
<!DOCTYPE html>
<html lang="zh-TW">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <title>Simple Demo 1</title>
</head>

<body>
  <h1>一個圖像將在3秒內出現，時間:
    <input id="time" value="0">
  </h1>
  <script>
    var c = 0;

    // 計時器
    function timedCount() {
      document.getElementById('time').value = c;
      c = c + 1;
      t = setTimeout("timedCount()", 1000);
    }
    timedCount();

    // Service Worker 註冊
    navigator.serviceWorker.register('/sw.js')
      .then(reg => console.log('Service Worker 註冊！', reg))
      .catch(err => console.log('Boo!', err));

    // 定時3秒
    setTimeout(() => {
      const img = new Image();
      img.src = '/dog.svg';
      document.body.appendChild(img);
    }, 3000);
  </script>
</body>

</html>
```

Service Worker JS（sw.js）：

```javascript
self.addEventListener('install', event => {
  console.log('v1 安裝...');

  // 取得 cat.svg
  event.waitUntil(
    caches.open('static-v1').then(cache => cache.add('/cat.svg'))
  );
});

self.addEventListener('activate', event => {
  console.log('v1 現在準備好處理提取！');
});

self.addEventListener('fetch', event => {
  const url = new URL(event.request.url);
  // 如果請求路徑相同於`/dog.svg`，將顯示來自於高速緩存(cache)的 cat.svg。
  if (url.origin == location.origin && url.pathname == '/dog.svg') {
    event.respondWith(caches.match('/cat.svg'));
  }
});
```
DEMO
![PWA 範例畫面 1](https://scontent.ftpe1-1.fna.fbcdn.net/v/t1.0-9/24058915_10208279952756002_8287519459444641964_n.jpg?oh=8869ccd49e34cbce91d29b05fecd9417&oe=5A8DA92D)
![PWA 範例畫面 2](https://scontent.ftpe1-1.fna.fbcdn.net/v/t1.0-9/24067897_10208279953156012_1900105887504626445_n.jpg?oh=a1f18c3c0560efcc329b0dad6784d177&oe=5A9DEDAC)

第一次開啟網頁上等待三秒後，出現 **狗狗** 圖片。Console 內會顯示**安裝…**、**Service Worker 註冊！**最後出現**現在準備好處理提取!**資訊。重新整理後透過 Console 觀察 **Service Worker** 就會攔截到圖片的 **Request**，並置換成 **貓咪** 的圖片。

---
## Chrome DevTools

開發 Progressive Web App 需要許多技術，包括 [Service Workers](https://developer.mozilla.org/zh-CN/docs/Web/API/Service_Worker_API) 、 [Web App Manifests](https://developer.mozilla.org/zh-TW/docs/Web/Manifest) 、 [Cache Storage API](https://developer.mozilla.org/en-US/docs/Web/API/CacheStorage) 、 [IndexedDB](https://developer.mozilla.org/zh-TW/docs/Web/API/IndexedDB_API/Basic_Concepts_Behind_IndexedDB) 和 [Push Notifications](https://developers.google.com/web/fundamentals/codelabs/push-notifications/?hl=zh-cn) ... 等等，於是 Google 很貼心的在Chrome 52版本之後的開發者模式（Chrome DevTools）裡面新增 **Application**，讓開發者能檢查與管理資訊。

![Chrome DevTools - Application](https://scontent.ftpe1-1.fna.fbcdn.net/v/t1.0-9/23905479_10208280040238189_3778533564807531069_n.jpg?oh=b58ccbf869fa803f4a5a3201c2e0952f&oe=5A994B80)

### Application

開啟 **Chrome DevTools** 的 **Application** 可以查看 **Application** 、 **Storage** 、 **Cache** 資訊。

Application 裡面有:
1. Manifest
1. Service Workers
1. Clear storage

#### Manifest

點選下圖左側的 Manifest 項目，我們可以看到右側顯示 manifest.json 文件的相關資訊，包括應用程式名稱、起始 URL、圖示等。

#### Service Workers

點選 Service Workers 項目，右側有一排複選框，分別介紹如下：

* Offline
  * 可以模擬無網路連線的環境。
  * 通常我們會拿來測試 Service Workers 『離線瀏覽網站』的需求是否成功。

* Update on reload
  * 如果開發者更新 service-worker.js，則新的 Service Workers 將會直接取代原本的 Service Workers。
* Bypass for network
  * 強迫瀏覽器忽略 Service Workers，直接從 network 獲取資源。
  * 如果你擔心 Service Worker 的快取將會返回舊的資源，則可以勾選這個項目，避免顯示舊的內容。
* Show all
  * 顯示所有 Service Workers

![Chrome DevTools - Application - Serbice Workers](https://scontent.ftpe1-1.fna.fbcdn.net/v/t31.0-8/23916325_10208280169281415_7436222569833412247_o.jpg?oh=c1f12d3dbe1a71dc3d4139f23df2b8e9&oe=5AA4C182)

#### Clear storage