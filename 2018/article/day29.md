## 設定localhost走SSL協定

昨天兩邊平台設定好後，想說試寫一下sample的登入，可是居然跑出請用加密的方式去載入api...
因為現在越來越注重隱私權了，網站送出去的內容如果沒有加密的話，很容易就會被攔截下來內容被看光光，所以許多知名的服務都要限定使用https來做連線，不然不是報錯就是警告跑出來...

在今年7月Google也發布Chrome瀏覽器的更新把未加密的網站都列入不安全裡，前端人員也要懂一些有關於SSL的觀念，在自己架網站上或者是開發上會有一定的幫助
> 相關閱讀
 - [Google 發布 Chrome 68，HTTP 網站全面標記為不安全](http://technews.tw/2018/07/25/google-chrome-68-http-website-not-secure/)
 - [使用 HTTPS 確保網站安全無虞](https://support.google.com/webmasters/answer/6073543?hl=zh-Hant)

