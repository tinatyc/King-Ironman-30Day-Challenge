## instascan的介紹
---

今天要大略解析一下instascan這個專案。
前幾天有Demo了我串[instascan](https://github.com/schmich/instascan)之後的成果[傳送門](https://ithelp.ithome.com.tw/articles/10205709)，主要是`實現跨平台可以實現一樣的功能- **使用網頁開啟相機掃描QRCode** `!

那麼[instascan](https://github.com/schmich/instascan)又是用什麼技術組成的呢？    
且待我略薄的分析一下....

### WebRTC

[WebRTC](https://webrtc.org/)的全名是「Web Real-Time Communication」- 網頁即時通訊
是為了實現跨平台、跨瀏覽器、在跨設備上都可以使用**網頁瀏覽器**來進行即時的影音通訊協定，這個計畫是由Google、Mozila和Opera所提倡並支援，並且為開源專案。

官方網站目前為Google來做維護，可以看到官網上有寫到WebRTC的使命
>**Our mission:** To enable rich, high-quality RTC applications to be developed for the browser, mobile platforms, and IoT devices, and allow them all to communicate via a common set of protocols.

我們到[Can I use](https://caniuse.com/)查詢WebRTC的支援度如下。
![Can I use_WebRTC](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day14_1.png?raw=true)
