## instascan的介紹
---

今天要大略解析一下instascan這個專案。
前幾天有Demo了我串[instascan](https://github.com/schmich/instascan)之後的成果[傳送門](https://ithelp.ithome.com.tw/articles/10205709)，主要是`實現跨平台可以實現一樣的功能- **使用網頁開啟相機掃描QRCode** `!

那麼[instascan](https://github.com/schmich/instascan)又是用什麼技術組成的呢？    
且待我略薄的分析一下....

---
   

> WebRTC

[WebRTC](https://webrtc.org/)的全名是「Web Real-Time Communication」- 網頁即時通訊
是為了實現跨平台、跨瀏覽器、在跨設備上都可以使用**網頁瀏覽器**來進行即時的影音通訊協定，這個計畫是由Google、Mozila和Opera所提倡並支援，並且為開源專案。

官方網站目前為Google來做維護，可以看到官網上有寫到WebRTC的使命
>**Our mission:** To enable rich, high-quality RTC applications to be developed for the browser, mobile platforms, and IoT devices, and allow them all to communicate via a common set of protocols.

     
我們到[Can I use](https://caniuse.com/)查詢WebRTC的支援度如下。
![Can I use_WebRTC_desktop](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day14_1.png?raw=true)

橘框框裡是比較偏向桌機板的瀏覽器，可以看到我們的古早味的IE是完全不支援的~~(IE必須死)~~，其他瀏覽器火狐Firefox、Chrome支援度都還不錯。
      
最重要是我們的手機瀏覽器來看一下支援度如何～
![Can I use_WebRTC_mobile](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day14_2.png?raw=true)   
    
iOS Safari 自從iOS11開始支援WebRTC
補充說明，在上面有說因為iOS和手機版的Safari是綁定在一起的，所以指的是`手機系統版本`。
![Can I use_WebRTC_iOS](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day14_3.png?raw=true)   
    
其餘像是Android Browser支援度也是都還蠻高的，在做Give Me Find專案的那時候還沒有到iOS11，只是剛要出而已....  
所以那時候就很傷腦筋，這樣iPhone不支援網站怎麼辦...要怎麼Demo啊！！(因為我是用iPhone手機)  蘋果不轉人來轉，於是就衍生了另外一種查詢的方式。   

我個人覺得WebRTC還蠻有趣的，將來應該是一個趨勢！   

因為物極必反！現在太多APP形成一種亂象，有點像是免洗APP的概念，想使用一種服務有太多可以選擇了....    
就是因為太多太亂，消費者不知道自己裝了什麼也不想冒險裝一個應用程式在手機裡！   
所以網頁應用需求上升，這東西將來應該蠻有發展潛力的，我要等我明年寫鐵人賽的時候再回來看是否像我說的一樣XD   

這裡有蠻多WebRTC的[Demo](https://webrtc.github.io/samples/)，這些我就不錄影了，請看官們自行用桌電和手機開起來玩玩看囉～
     
   
> ZXing

[ZXing](https://github.com/zxing/zxing)有點像是負責解碼的程式，為一個JAVA的library，同樣是開源的程式碼，圖像解析一維和二維的條碼，具有其他程式語言的接口提供串接。（~~不負責的看圖說故事XD~~）    
    
附帶小知識：[條碼的種類](http://www.appsbarcode.com/barcode-type.php)

~~老實說我對這個不太了解，就草草帶過吧...大致上知道他是幹嘛的就好了（大誤~~

---

### 實際應用

現在我們要來實際的Coding一下instascan這個專案，來完成我們的目標-開啟網頁掃描QRCode
請搭配github服用：(https://github.com/schmich/instascan )

首先你必須在網頁裡掛載[`instascan.min.js`](https://github.com/schmich/instascan/releases/download/1.0.0/instascan.min.js)

```
<script type="text/javascript" src="instascan.min.js"></script>
```

github裡有提供完整的範例html，講解一下

```
<!DOCTYPE html>
<html>
<head>
    <title>Instascan</title>
    <script type="text/javascript" src="instascan.min.js"></script>
    <!-- 載入instascan.min.js -->
</head>

<body>
    <video id="preview"></video>
    <!-- 詢問是否允許開啟相機後，會顯示在這個元素裡 -->
    <!-- ---------- -->
    <!-- 以下程式面 -->
    <script type="text/javascript">
    let scanner = new Instascan.Scanner({
        video: document.getElementById('preview')
    });
    // 開啟一個新的掃描
    // 宣告變數scanner，在html<video>標籤id為preview的地方開啟相機預覽。
    // Notice:這邊注意一定要用<video>的標籤才能使用，詳情請看他的github API的部分解釋。

    scanner.addListener('scan', function(content) {
        console.log(content);
    });
    //開始偵聽掃描事件，若有偵聽到印出內容。

    Instascan.Camera.getCameras().then(function(cameras) {
    //取得設備的相機數目
        if (cameras.length > 0) {
          ///若設備相機數目大於0 則先開啟第0個相機(程式的世界是從第零個開始的)
            scanner.start(cameras[0]);
        } else {
          //若設備沒有相機數量則顯示"No cameras found";
          //這裡自行判斷要寫什麼
            console.error('No cameras found.');
        }
    }).catch(function(e) {
        console.error(e);
    });
    </script>
</body>
</html>
```
做出來的成品就會像這樣
